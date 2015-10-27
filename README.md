# Cài đặt apache làm webserver

#I. Giới thiệu

##A. Quá trình phát triển

- Apache web Server đi vào thế giới Server từ giữa những năm 90. Một nhà lập trình đã nhận định: "Apache như là một viên đá quý của chương trình mã nguồn mở, chi phí cho nó thì hầu như không có, hoạt động tốt hơn những đối thủ cạnh tranh khác, do đó nó được sử dụng ngày càng rộng rãi hơn nhũng Web Servers thương mại khác".

- Apache thường đi kèm với bản phân phối Linux hoặc tải từ trang ww.apache.org để được dùng bản mới nhất.

- Apache thống trị thị trường web Server từ rất sớm.

##B. Tiến trình giải quyết yêu cầu và đặc điểm Apache

- Web Server là sự kết hợp giữa phần cứng và phần mềm phục vụ cho những tài liệu HTTP khi client yêu cầu. Một web Server cơ bản là môt máy tính với hệ điều hành Linux, một file hệ thống đầy đủ khả năng hỗ trợ tốt cho ứng dựng Web Server, và một kết nối mạng (đó là đặc trưng cho Internet hoặc tổ chức Intranet). Khi làm việc với web server cần có sự cân nhắc về loại người dùng đảm bảo hệ thống chạy thực sự hiệu quả, như là:

+ Mục đích của Web Server có thể thay đổi. Từ đơn giản như mạng server nội bộ, đến phức tạp như e-commerce server. Nó rất quan trọng để xác định mục đích Server trước khi xây dựng và đưa vào hoạt động

+ Tiến trình request/response bắt đầu từ việc client yêu cầu, thường là từ trình duyệt Web, và sự trả lời từ Server, trả về thông tin cho Client

- Tiến trình hoạt động Web Server

+ Client sử dụng trình duyệt Web kết nối đến Server và đưa ra yêu cầu. Yêu cầu này sử dụng giao thức HTTP mà người dùng muốn Server cung cấp và nói cho Server biết phiển bảo nào HTTP dùng để trả lời. Web Server lắng nghe những yêu cầu trên mạng. Khi một yêu cầu được gửi đến, Web Server phân tích thành 3 thành phần:
<ul>
<li>Cách thức sử dụng là GET, POST hay HEAD. Phương pháp GET yêu cầu Uniform Resource Indicator (URI - Sự chỉ định tài nguyên đồng nhất) hoặc tài liệu từ Web Server. Phương pháp POST gửi dữ liệu điều khiển chỉ định bởi URI. Phương pháp HEAD chỉ yêu cầu headers từ Web server.</li>
<li>Tài nguyên đang được yêu cầu: Web Server đổi URI, xác định đói tương yêu cầu thành đường dẫn vật lý trên hệ thống file của Web Server</li>
<li>Phiên bản HTTP</li>
</ul>
+ Web server tiếp tục quy trình giải quyết yêu cầu bằng việc dùng Child Processes (tiến trình con) để hoàn thành yêu cầu, và gửi trả lời lại cho người dùng. Trong khoảng thời gian đó Web Server sẽ kiểm tra quyền hạn của Client. Trước khi hoàn tất yêu cầu, Web Server sẽ xác định loại MIME của đối tượng được yêu cầu và sắp đặt lại aliases

+ Yêu cầu Client đã được thực hiện. Trình duyệt Web sẽ cập nhập thông tin. Ví dụ một trang HTML, một file, một thông báo lỗi sẽ xuất hiện. Khi kết thúc yêu cầu Web Server sẽ cập nhập lại file log và ngắt kết nối đến Client.

- Đặc điểm của Web Server
<ul>
<li>Là phần mềm mã nguồn mở và hoàn toàn miễn phí. Hỗ trợ trên những hệ điều hành khác nhau.....</li>
<li>Apache là một Modular, dễ lựa chọn và có thể tích hợp với sản phẩm khác như IBM Websphere</li>
</ul>

#II. Cài đặt và cấu hình

- Trước khi làm việc ở Ubuntu, nên tiến hành cập nhập gói phần mềm của Ubuntu lên phiên bản mới nhất với lệnh:

**apt-get update**
<img src="http://prntscr.com/8vi9rg" >

- Tên phần mềm Apache trên Ubuntu là apache2 nên sẽ cài đặt với lệnh sau:

**apt-get install apache2**
<img src="http://prntscr.com/8via5r" >

- Cài đặt trong thì truy cập vào địa chỉ Ip của máy chủ, sẽ thấy trang chào mừng của Apache
<img src=http://prntscr.com/8vib2b>

###Cấu trúc thư mục cấu hình Apache trên Ubuntu

- **/etc/apache2/conf-available/** : Thư mục này sẽ chứa các file thiết lập cấu hình sẵn của Apache trên Ubuntu, nhưng thiết lập trong đây sẽ chưa được áp dụng vì Ubuntu không load được thiết lập trong thư mục này.

- **/etc/apache2/conf-enabled/** : Thư mục chứa các file thiết lập cấu hình của Apache trên Ubuntu đang được bật. Hãy hiểu là nếu thưc mục này có một iên kết tượng trưng (symlink) qua một file module nào đó bên thư mục conf-available thì nó sẽ được bật.
- **/etc/apache2/mods-available/** : Thư mục chứa các file từng module của Apache trên Ubuntu nhưng chưa được bật.
- **/etc/apache2/mods-enabled/** : Thư mục chứa các file từng module của Apache trên Ubuntu đang được bật.
- **/etc/apache2/site-available/** : Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu nhưng chưa được bật
- **/etc/apache2/site-enabled/** : Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu đang được bật
- **/etc/apache2/apache.conf** : File cấu hình Apache trên Ubuntu
- **/etc/apache2/envvars** : File thiết lập các biến với giá trị có sẵn để sử dụng các file cấu hình.
- **/etc/apache2/magic** : File thiết lập mod_mime_magic trên Apache.
- **/etc/apache2/ports.conf** : File cấu hình cổng mạng của Apache (mặc định là Port 80)

##Thư mục gốc chứa dữ liệu website của Apache trên Ubuntu

- Mặc định, Apache trên Ubuntu sẽ sử dụng thư mục  /var/www/html để chứa dữ liệu website gốc (load bằng IP hoặc hostname). Khi vào đây sẽ thấy một file index.html. đó chính là giao diện Apache Welcome đã thấy ở trên.

##Thêm VirtualHost (thêm domain) vào Apache trên Ubuntu

- Cách thêm VirtualHost của Apache trên Ubuntu sẽ khác so với CentOS. Trước tiên, chúng ta cũng cần tạo cho nó một thư mục chứa dữ liệu cho domain cần thêm vào

	**mkdir -p /home/hunter.com/public_html**
	**mkdir -p /home/hunter.com/log**

- Sau đó chúng ta cần copy file /etc/apache2/sites-available/000-default.conf ra một file mới file chứa cấu hình của domain cần thêm vào (hunter.com)
Lưu ý: Có thể file cấu hình mặc định của bạn không phải tên là default mà là “000-default.conf” nên tốt nhất bạn nên vào thư mục /etc/apache2/sites-available/ để xem rồi copy cho đúng.
Bây giờ hãy mở file /etc/apache2/sites-available/thachpham.dev.conf lên và sửa nội dung trong đó cho nó gọn hơn như thế này:

	'<VirtualHost *:80>
	        ServerName thachpham.dev
	        ServerAlias www.thachpham.dev
	        ServerAdmin contact@thachpham.com
	 
	        DocumentRoot /home/thachpham.dev/public_html
	 
	        <Directory /home/thachpham.dev/public_html>
	                Options FollowSymLinks
	                AllowOverride All
	                Order allow,deny
	                Allow from all
	                Require all granted
	        </Directory>
	 
	        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
	        # error, crit, alert, emerg.
	        # It is also possible to configure the loglevel for particular
	        # modules, e.g.
	        LogLevel error
	 
	        ErrorLog /home/thachpham.dev/log/error.log
	        CustomLog /home/thachpham.dev/log/access.log combined
	 
	        # For most configuration files from conf-available/, which are
	        # enabled or disabled at a global level, it is possible to
	        # include a line for only one particular virtual host. For example the
	        # following line enables the CGI configuration for this host only
	        # after it has been globally disabled with "a2disconf".
	        #Include conf-available/serve-cgi-bin.conf
	</VirtualHost>
	 
	# vim: syntax=apache ts=4 sw=4 sts=4 sr noet'
Nhớ thay:

	* SererName – Domain website cần thêm vào.
	* ServerAlias – Sử dụng một tên domain khác thay thế, hay còn gọi là Parked Domain nếu bạn đã từng sử dụng qua cPanel đó.
	* DocumentRoot – Đường dẫn tới thư mục chứa dữ liệu website của domain này mà ta đã tạo ở trên.
	* ErrorLog – Đường dẫn tới thư mục log đã tạo ở trên cho domain này.
	* CustomLog – Tương tự ErrorLog nhưng sẽ lưu log lại các lượt truy cập với file là access.log.

Sau đó chúng ta gõ lệnh sau để nó tự động tạo ra một symlink của file này vào thư mục sites-enabled để bật nó lên.

	**a2ensite thachpham.dev**

Hãy nhớ rằng, thachpham.dev.conf là tên file cấu hình trong thư mục sites-available đã bỏ đuôi .conf.
Kết quả trả về:

root@vps103534:~# a2ensite thachpham.dev
Enabling site thachpham.dev.
To activate the new configuration, you need to run:
service apache2 reload
Gõ lệnh sau để khởi động lại Apache.

service apache2 restart
Bây giờ nếu bạn truy cập domain vừa thêm vào nó sẽ hiển thị ra lỗi 403 do thư mục của domain chứa có tập tin index để nó load. Hãy tạo ra một file index.html với nội dung sau và upload vào thư mục public_html của domain vừa thêm.

<html>
<head></head>
<body><h1>Tao VirtualHost Thanh Cong! </h1></body>
</html>
Kết quả:

Nếu bị lỗi 500
Nếu bạn vào website mà bị lỗi 500 (dễ gặp ở Ubuntu 10.04 32-bits), hãy mở lại file cấu hình virtualhost của bạn và xóa đoạn này đi:

Order allow,deny
Allow from all
Require all granted
I.4) Bật module mod_rewriteNếu bạn sử dụng WordPress sau này hay các website khác có sử dụng mod_rewrite để ghi lại đường dẫn thì phải bật module này lên. Ở phần thêm VirtualHost, chúng ta đã thêm AllowOverride All vào thiết lập thư mục gốc của domain rồi, nhưng chúng ta cũng cần bật module rewrite lên nữa. Hãy gõ lệnh sau:

a2enmod rewrite
Và khởi động lại Apache

service apache2 restart

Mô hình apache core

Mô hình Apache core

Apache core:

http_protocol.c: chứa các procedure để giao tiếp với clinet thông qua giao thức http. Mọi thứ trao đổi với clinet do thằng này đảm nhiệm
http_main.c :khởi động server, tạo vòng lặp chính để đợi + chấp nhận các kết nối, và quản lý toàn bộ timeout
http_request.c: quản lý tiến trình xử lý bản tin request, đảm bảo chuyển các bản tin điều khiển tới các modul phù hợp theo đúng thứ tự + quản lý lỗi xảy ra trên server
http_core.c: triển khai các chức năng cơ bản nhất trên Apache
alloc.c: kiểm soát việc phân chia tài nguyên và lưu trữ các thông tin về sự phân chia đó
http_config.c: xử lý file cấu hình và hỗ trợ virtual host + liệt kê các modul sử dụng trong apache
2.    Request processing – luồng request, cách xử lý một request từ phía cinet

Cách xử lý được thực hiện theo trình tự sau:

1, Phân giải địa chỉ
2, Kiểm tra truy cập và cấp quyền truy cập đến những tài nguyên cần thiết
3, Xác định MIME (Multipurpose Internet Mail Extensions) của đối tượng truy vấn. Tức là thông tin về kiểu định dạng của tài nguyên trên server được gọi tên trong gói HTTP Request
4, Chỉnh sửa lại một số thông tin ( ví dụ thay đổi Alisa thành một đường dẫn thực – định nghĩa trong modul alisa thuộc phần mod_alisa)
5, Gửi lại dữ liệu cho clinet
6, Ghi lại log
3.    Communicating between modules – giao tiếp giữa các module

Các modules không giao tiếp trực tiếp với nhau mà thông qua core.

4.    Handler

Handler là một hành động được Apache định nghĩa riêng cho từng loại file nhất định. Mặc định, tùy loại file mà sẽ được xử lý theo các cách khác nhau
Handler có thể được cấu hình dựa trên phần mở rộng của file hoặc theo từng thư mục
Mặc định, có 7 loại handler:
Send-as-is: dùng trong module mod_asis, dùng để gửi trả gói tin cho clinet mà không sử dụng đầy đủ HTTP header
Cgi-script: coi file là một cgi-script (tương ứng modul: mod_cgi)
Imap-file sử dụng chung với mod_imagemap
Server-info: lấy thông tin về cấu hình của server
Server-status: lấy thông tin về trạng thái của server
Type – map: sử dụng cùng với module mod_negotiation
Default-handler: gửi file sử dụng default_handler()
Ví dụ:
Thay đổi nội dung mặc định với CGI script:
Đoạn mã sau sẽ tác động lên các tập tin html, để kích hoạt lên tập tin footer.pl
Action add-footer /cgi-bin/footer.pl
AddHandler add-footer .html

Sau đó, các tập tin CGI sẽ gửi các tài liệu theo yêu cầu (tại biến PATH_TRANSLATED) và thực hiện bất của yêu cầu nào mong muốn

File với HTTP header
Với send-as-is handler, được kích hoạt như sau:

<Directory /web/htdocs/asis>
SetHandler send-as-is
</Directory>

Khi đó tất cả các file trong /web/htdocs/asis sẽ được xử lý, bất kể đuôi là gì

Chú ý lập trình:
Để thực hiện các tính năng, chúng ta sẽ bổ sung vào bằng cách dùng Apache API , cụ thể, chúng ta sẽ thêm vào cấu trúc request_rec theo cấu trúc:

Char*handler;

Nếu muốn có một modul tham gia vào xử lý, thiết lập thêm r->handler, và phải thêm vào trước khi trình xử lý invoke_handler được yêu cầu.

5.    Modules

Các mdoul được cài đặt sẵn trong quá trinh buil Apache, hoặc có thể add thêm.

Mặc định sẵn sẽ có các modules như sau – các modul này sẽ hoạt động lần lượt theo request của người dùng (6 bước, xem lại ở mục 2 – request processing)

1, chuyển đổi giữa các URI thành filename trên server:
Mod_userdir: chuyển thư mục home cho từng user
Mod_rewrite: điều chỉnh lại đường dẫn URL
2, Giai đoạn Xác thực/ Phân quyền:
Mod_ahth, mod_auth_anon, mod_auth_db, mod_ahth_dbm: các kiểu xác thực người dùng
Mod_access: kiểm soát truy cập theo từng host
3, Xác định MIME của đối tượng được truy vấn:
Mod_mime: xác định loại file bằng cách dựa vào phần mở rộng
Mod_mime_magic: xác định loại file bằng cách sử dụng magic number
4, chỉnh sửa đường dẫn:
Mod_alias: thay thế alias bằng đường dẫn thực trên server
Mod_env: thay đổi các tham số hệ thống dựa trên thông tin trong file cấu hình
Mod_spelling: tự động sửa lỗi trông URL
5, gửi trả lại cho clinet
Mod_actions: các scrip cho từng loại file sẽ được thực thi
Mod_asis: gửi file nguyên dạng
Mod_autoindex:
Mod_cgi: gọi scrip CGI và trả lại kết quả
Mod_include:
Mod_dir: xử lý về thư mục
Mod_imap: xử lý về image-map file
6, ghi log:
Mod_log_*: các modul log khác nhau
Gồm 3 thành phần chính:
1, Global Evironment: các thông số để cấu hình điều khiển hoạt động của toàn bộ ApacheServer
2, Các directive định nghĩa các thông số của “main” hay “default” server
6.    Apache configuration File

Khi một request đến Apache server mà không được virtual host nào xử lý thì các thông số này sẽ quyết định hành động của ApacheServer. Các tham số này cũng đồng thời xác lập các giá trị mậc định cho tất cả các Virtual host

3, Các tham số riêng cho từng virtual host
6.1 Config/ Global enviroment:

1, ServerToken & ServerSignature
ServerSignature Off

ServerTokens Prod

Giảm nguy cơ bị lộ thông tin về phiên bản Apache đang chạy trên server (chỉ là giảm thôi nhá)

2, Server Root: cấu hình thư mục lưu trữ chính của Apache
3, PidFile: thông số này lưu trữ đường dẫn đến file httpd.pid, là file lưu trữ process ID của Apache mỗi khi khởi chạy. Mặc định, file này nằm ở /etc/httpd/run/httpd.pid và trong đó chỉ có 1 con số (ví dụ: 1231)
4, Timeout: thời gian tim out cho hệt hống, giá trị mặc định
5, KeepAlive
KeepAlive là một hình thức có thể giúp tăng tốc độ tải trang khi không mở kết nối cho từng request một. Tuy nhiên, khi bị tấn công Ddos, thì nên tắt chắc năng này để giảm thiểu ảnh hưởng tới hệ thống. Nhưng với CDN thì có lẽ nên bật vì số lượng Edge rõ lắm. Thông số KeepAlive cho phép kiểu kết nối này được bật hay không.

Thông số KeepAliveTimeOut

6, Listen: cấu hình địa chỉ IP và port để Apache nhận các gói request
7, LoadModul: gọi modul nào sẽ khởi động cùng hệ thống
8, Include: cấu hình thư mục chứa file config
1, ServerAdmin: cấu hình địa chỉ email của người quản trị, sẽ hiển thị trên một số trang (như trang báo lỗi 404)
2, UseCanonicalName: thông thường, khi sử dụng Name-based Virutal Host thì nên set là off – không hỉu
3, DocumentRoot: thư mục lưu trữ các đường dẫn chứa mã nguồn của website, các requet từ clinet sẽ chỉ truy xuất thông tin từ thư mục này.
Windows: c:/wampp/www
Centos: /var/www/html/
4, DirectoryIndex: chỉ định file mặc định được trả về cho clinet khi có request tới một thư mục nào đó, thông thường các file như index.html, index.php sẽ được sử dụng.
6.2 Config/ Main Server Configuration

DirectoryIndex index.htm index.html index.html.var
5, AccessFileName: chỉ định file bổ sung các cấu hình riêng cho từng thư mục nhất định. Thông thường sẽ là file “.htaccess” – file này trong mỗi virutalhost sẽ có, nói lên việc truy cập, blah blah…
6, TypesConfig: chỉ đường dẫn tới file mime.types. File này sẽ giúp cho Apache tra cứu phần mở rộng của file để xác định MIME type trong HTTP Header (xem lại phần ví dụ handler)
DefaultType  text/plain

Mặc định, MIME type cho các file apache không xác định được sẽ là kiểu file text

7, HostnameLookups: cấu hình ghi log tên hostname của clinet hay chỉ đại chỉ IP của clinet (thường mặc định để off)
8, ErrorLog: cấu hình đường lưu trữ Error của hệ thống
9, LogLevel: mức độ ghi log. Giống như syslog, log trong Apache cũng được ghi thành 7 mức độ khác nhau từ cao xuống thấp là:
Emergency
Alert
Critical
Error
Warning
Notification
Information
Debug
10, Log
Dùng cái này để chạy nhiều site trên cùng một server.
Có 2 loại cấu hình
IP-based VirtualHost: trỏ từng website vào các địa chỉ IP (trên server có nhiều hơn 1IP)
Name-based Virtual Host: thông tin hostname được lưu trong phần Header của bản tin HTTP Request. Khi nhận các bản tin Request này, thì apache sẽ chuyển đến các virtual host tương ứng (cần 1 IP thôi)
Các vitual host được thực hiện trong file httpd.conf hoặc file httpd-vhost.conf. Với các thành phần cụ thể như sau:
Đường dẫn tới thư mục lưu trữ web
Server name
Đường dẫn tới log
6.3 Apache Virtual Host

Ví dụ:

<VirtualHost *:80>
DocumentRoot /www/example1

ServerName www.example.com

# Other directives here

</VirtualHost>

<VirtualHost *:80>

DocumentRoot /www/example2

ServerName www.example.org

# Other directives here

</VirtualHost>

 

Xem thêm tại đây
6.4 Một số trường – cấu hình apache server

Các thông số trong http.conf
Server Root: chỉ dẫn vị trí cài đặt Apache
Cú pháp : ServerRoot <vị trí cài đặt Apache>

Listen : quy định địa chỉ IP hoặc cổng mà Apache nhận kết nối từ client
Cú pháp: listen <port/IP>

Server Admin:địa chỉ mail của người quản trị hệ thống
Cú pháp: ServerAdmin <địa chỉ email>

Server name: tên máy tính của server
Cú pháp: ServerName <tên máy server>ort

DocumentRoot: lưu trữ nội dung của website, web server lấy lấy những tập tin trong thư mục (htdocs) phục vụ cho yêu cầu của client
Cú pháp: DocumentRoot <đường dẫn thư mục>

DirectoryIndex:các tập tin mặc định được truy vấn khi truy cập web
Cú pháp: DirectoryIndex <danh sách các tập tin>

Error Log :chỉ ra tập tin để server ghi vào những lỗi mà nó gặp phải
Cú pháp:ErrorLog <vị trí log>

Alias:ánh xạ đường dẫn cục bộ(không nằm trong document) thành đường dẫn địa chỉ URL
Cú pháp:alias<đường dẫn http><đường dẫn cục bộ>

7.    Mutiprocessing

Có 2 khái niệm về khả năng xử lý của webserver

Single-threaded web server: không có khả năng xử lý đồng thời nhiều request một lúc
Multi-thread web server: có khả năng xử lý nhiều request một lúc, gồm 2 kĩ thuật chính là :
Multi-process: tạo process cho từng request, có 2 loại chủ yếu
Prefork: tạo các process riêng biệt. Lỗi trên 1 process không gây ảnh hưởng tới process khác
Multi-thread: tạo Thread mới cho từng request
Worker: tạo các thread riêng biệt cho request, hợp với đa lõi, nhưng nếu có 1 thread bị lỗi sẽ có thể gây ảnh hưởng tới các thread trong cùng process đó
Đánh giá chung: Thread thì tiết kiệm tài nguyên hơn là Process. Nhưng còn tùy thuộc vào các yếu tố khác nhau, ví dụ PHP thì nên dùng Prefork, vì nó không ổn định với hình thức chia sẻ bộ nhớ chung (Process thì sẽ tạo tài nguyên riêng cho từng process, nên sẽ không bị ảnh hưởng khi dùng PHP). (Thread dùng chung bộ nhớ, tài nguyên à ảnh hưởng)

( tra thêm tài liệu để hiểu rõ sự khác biệt giữa process và thread)
