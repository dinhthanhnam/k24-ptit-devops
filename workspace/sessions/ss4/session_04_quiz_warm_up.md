---
schema_version: 1
id: ss04_quiz_warm_up
type: quiz
status: draft
course_id: devops-basic
session: 4
unit: 0
title: Quiz Warm-up Session 04
session_kind: theory
tags: []
concepts: []
depends_on:
- ss04_lesson_01
- ss04_lesson_02
- ss04_lesson_03
- ss04_lesson_04
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover: []
source: generated
pm_ref: Session 04 / quiz_warm_up
language: vi
created: '2026-07-17'
updated: '2026-07-17'
quiz_kind: warm_up
question_count: 30
maps_to:
- ss04_lesson_01
- ss04_lesson_02
- ss04_lesson_03
- ss04_lesson_04
---

# Quiz Warm-up Session 04

## Q1
Trong hệ điều hành Linux, lệnh nào dưới đây được sử dụng để thay đổi quyền truy cập (đọc, ghi, thực thi) của một tệp tin?

[A]
`chmod`
[EXP]
Đúng. Lệnh `chmod` (change mode) dùng để thay đổi quyền truy cập tệp tin cho owner, group và others.
[B]
`chown`
[EXP]
Lệnh `chown` dùng để thay đổi chủ sở hữu (owner) và nhóm sở hữu (group) của tệp tin.
[C]
`chroot`
[EXP]
Lệnh `chroot` dùng để thay đổi thư mục gốc ảo cho tiến trình hiện hành, không liên quan đến quyền file.
[D]
`chsh`
[EXP]
Lệnh `chsh` dùng để thay đổi shell mặc định đăng nhập của người dùng hệ thống.

@correct: A
@point: 3.3
@difficulty: 4
@concept: linux-basics
@category: 0

## Q2
Để tìm kiếm một chuỗi ký tự cụ thể nằm trong nội dung của các tệp tin văn bản ở thư mục hiện hành, lệnh nào sau đây phù hợp nhất?

[A]
`find`
[EXP]
Lệnh `find` chỉ dùng để tìm kiếm vị trí tệp tin và thư mục theo tên, kích thước, thời gian chứ không tìm nội dung bên trong file.
[B]
`grep`
[EXP]
Đúng. Lệnh `grep` dùng để lọc và hiển thị các dòng văn bản có chứa chuỗi ký tự khớp với mẫu tìm kiếm bên trong file.
[C]
`locate`
[EXP]
Lệnh `locate` dùng để tìm nhanh đường dẫn tệp tin dựa trên cơ sở dữ liệu hệ thống được lập chỉ mục trước.
[D]
`whereis`
[EXP]
Lệnh `whereis` dùng để tìm vị trí của các file thực thi (binary), mã nguồn và trang hướng dẫn sử dụng của một lệnh.

@correct: B
@point: 3.3
@difficulty: 4
@concept: linux-basics
@category: 0

## Q3
Trong shell Linux, khi bạn chạy một lệnh hoặc kịch bản kèm theo ký tự `&` ở cuối dòng (ví dụ: `./backup.sh &`), tiến trình đó sẽ được thực thi như thế nào?

[A]
Tiến trình chạy ở chế độ foreground và chặn mọi thao tác tiếp theo trên terminal.
[EXP]
Nếu chạy ở foreground thì terminal sẽ bị chặn cho đến khi lệnh thực thi xong, không cần thêm ký tự `&`.
[B]
Tiến trình bị tạm dừng ngay lập tức và chuyển vào danh sách hàng đợi của hệ thống.
[EXP]
Ký tự `&` không tạm dừng tiến trình mà vẫn cho phép tiến trình tiếp tục chạy trực tiếp.
[C]
Tiến trình chạy ẩn dưới nền (background) giúp giải phóng terminal để tiếp tục gõ lệnh khác.
[EXP]
Đúng. Ký tự `&` yêu cầu shell chạy tiến trình ở dạng background để người dùng có thể sử dụng tiếp terminal.
[D]
Tiến trình được chạy với đặc quyền quản trị cao nhất tương đương với lệnh sudo.
[EXP]
Ký tự `&` không làm thay đổi đặc quyền user thực thi lệnh.

@correct: C
@point: 3.3
@difficulty: 4
@concept: linux-basics
@category: 0

## Q4
Khi tiến hành cấu hình bảo mật dịch vụ SSH bằng cách thay đổi cổng kết nối mặc định của SSH Daemon, học viên cần chỉnh sửa tệp tin cấu hình nào sau đây?

[A]
`/etc/ssh/ssh_config`
[EXP]
Tệp `ssh_config` dùng để cấu hình các thiết lập cho client khi thực hiện kết nối SSH từ máy này sang máy khác.
[B]
`/etc/ssh/sshd_identity`
[EXP]
Không tồn tại tệp tin này trong cấu hình mặc định của hệ thống dịch vụ SSH.
[C]
`/etc/ssh/ssh_host_key`
[EXP]
Tệp tin này chứa khóa mã hóa định danh của host server, không dùng để cấu hình cổng port của daemon.
[D]
`/etc/ssh/sshd_config`
[EXP]
Đúng. Tệp `/etc/ssh/sshd_config` chứa toàn bộ cấu hình hoạt động của SSH Daemon (server side), bao gồm cấu hình Port.

@correct: D
@point: 3.3
@difficulty: 5
@concept: infrastructure-security
@category: 0

## Q5
Để cấu hình cho phép đăng nhập vào VPS qua SSH không cần mật khẩu, học viên phải đặt nội dung khóa công khai (Public Key) local của mình vào tệp tin nào trên VPS?

[A]
`~/.ssh/authorized_keys`
[EXP]
Đúng. Khóa công khai của client phải được ghi nhận vào tệp `~/.ssh/authorized_keys` trên VPS của user tương ứng để xác thực kết nối.
[B]
`~/.ssh/id_ed25519.pub`
[EXP]
Tệp `id_ed25519.pub` lưu khóa công khai được sinh ra trên chính VPS, không phải nơi chứa khóa của client kết nối tới.
[C]
`~/.ssh/known_hosts`
[EXP]
Tệp `known_hosts` dùng để lưu trữ fingerprint xác nhận danh tính của các server remote mà client từng kết nối.
[D]
`~/.ssh/config`
[EXP]
Tệp `config` dùng để cấu hình cấu trúc host, bí danh (alias) kết nối nhanh ở phía client.

@correct: A
@point: 3.3
@difficulty: 5
@concept: infrastructure-security
@category: 0

## Q6
Khi muốn chạy hai website độc lập trên cùng một máy chủ Nginx bằng cách lắng nghe ở hai cổng port khác nhau (ví dụ: 8080 và 8090), học viên cần làm gì?

[A]
Tạo một server block duy nhất và khai báo cả hai cổng port vào cùng một dòng listen.
[EXP]
Một khối server block chỉ đại diện cho một logic cấu hình chạy ứng dụng, không nên khai báo chung chồng chéo như vậy.
[B]
Tạo hai khối server block riêng biệt, mỗi khối cấu hình listen cổng tương ứng và trỏ root về thư mục code riêng.
[EXP]
Đúng. Mỗi server block lắng nghe cổng riêng biệt và định cấu hình thư mục gốc (root directory) chứa mã nguồn của website đó.
[C]
Cấu hình một server block duy nhất lắng nghe cổng 80 và dùng rewrite rule để phân luồng.
[EXP]
Cách này không đáp ứng được yêu cầu lắng nghe kết nối trực tiếp ở hai cổng 8080 và 8090.
[D]
Khởi động hai service Nginx độc lập trên hệ thống VPS để quản lý hai cổng khác nhau.
[EXP]
Một hệ điều hành chỉ chạy duy nhất một tiến trình service Nginx để quản lý nhiều cấu hình server blocks.

@correct: B
@point: 3.3
@difficulty: 5
@concept: nginx-setup
@category: 0

## Q7
Để cấu hình Nginx chuyển hướng vĩnh viễn (Permanent Redirect) toàn bộ traffic từ giao thức HTTP sang HTTPS, mã phản hồi HTTP nào cần cấu hình kèm theo?

[A]
Mã phản hồi `302 Found`
[EXP]
Mã `302` biểu thị chuyển hướng tạm thời, các công cụ tìm kiếm sẽ không cập nhật lại liên kết vĩnh viễn của trang web.
[B]
Mã phản hồi `307 Temporary Redirect`
[EXP]
Mã `307` là chuyển hướng tạm thời giữ nguyên phương thức yêu cầu, không dùng cho chuyển hướng vĩnh viễn HTTP sang HTTPS.
[C]
Mã phản hồi `301 Moved Permanently`
[EXP]
Đúng. Mã `301` chỉ định chuyển hướng vĩnh viễn, báo cho trình duyệt và các công cụ tìm kiếm chuyển hẳn sang địa chỉ HTTPS mới.
[D]
Mã phản hồi `308 Permanent Redirect`
[EXP]
Mã `308` mặc dù là chuyển hướng vĩnh viễn nhưng không phổ biến và tương thích tốt như mã `301` truyền thống.

@correct: C
@point: 3.3
@difficulty: 6
@concept: nginx-setup
@category: 0

## Q8
Trong tệp cấu hình Server Block của Nginx, chỉ thị (directive) nào được sử dụng để khai báo tên miền (domain name) hoặc địa chỉ IP mà khối cấu hình đó sẽ áp dụng để xử lý yêu cầu?

[A]
`listen`
[EXP]
Chỉ thị `listen` chỉ định địa chỉ IP và cổng port mà server block sẽ lắng nghe kết nối, không dùng để khai báo tên miền.
[B]
`root`
[EXP]
Chỉ thị `root` chỉ định đường dẫn thư mục gốc trên đĩa cứng chứa các tệp tin mã nguồn tĩnh của website.
[C]
`index`
[EXP]
Chỉ thị `index` khai báo tên các tệp tin mặc định (như index.html, index.php) sẽ được trả về khi người dùng truy cập thư mục.
[D]
`server_name`
[EXP]
Đúng. Chỉ thị `server_name` được sử dụng để định cấu hình tên miền hoặc địa chỉ IP nhằm đối khớp và định tuyến yêu cầu HTTP truy cập vào đúng server block.

@correct: D
@point: 3.3
@difficulty: 5
@concept: nginx-setup
@category: 0

## Q9
Để cấu hình Nginx trả về một trang HTML tùy biến khi xảy ra lỗi `404 Not Found`, học viên cần khai báo chỉ thị cấu hình nào?

[A]
`error_page 404 /custom_404.html;`
[EXP]
Đúng. Chỉ thị `error_page` định nghĩa mã lỗi HTTP và liên kết tới trang giao diện HTML tùy biến mà bạn đã viết.
[B]
`custom_error 404 /custom_404.html;`
[EXP]
Không tồn tại chỉ thị cấu hình tên là `custom_error` trong cú pháp của Nginx.
[C]
`rewrite 404 /custom_404.html;`
[EXP]
Chỉ thị `rewrite` dùng để viết lại đường dẫn URL dựa trên biểu thức chính quy, không thiết kế để xử lý mã lỗi HTTP.
[D]
`try_files $uri 404 =/custom_404.html;`
[EXP]
Cú pháp này sai quy chuẩn của `try_files` và không giải quyết được nhu cầu trả lỗi tùy biến chuẩn xác.

@correct: A
@point: 3.3
@difficulty: 4
@concept: nginx-setup
@category: 0

## Q10
Khi kiểm tra nhật ký truy cập của Nginx (`access.log`), học viên phát hiện một dòng log ghi nhận mã phản hồi HTTP là `403` khi người dùng cố gắng truy cập vào một thư mục trên website. Mã lỗi này biểu thị điều gì?

[A]
Yêu cầu truy cập của người dùng được máy chủ xử lý thành công và tệp tin đã được tải về trình duyệt.
[EXP]
Yêu cầu xử lý thành công sẽ được ghi nhận bằng mã phản hồi HTTP `200 OK`, không phải `403`.
[B]
Yêu cầu truy cập bị cấm (Forbidden), thường do phân quyền tệp tin trên hệ điều hành VPS chưa đúng hoặc cấu hình chặn quyền truy cập của Nginx.
[EXP]
Đúng. Mã phản hồi `403 Forbidden` chỉ ra rằng máy chủ hiểu yêu cầu nhưng từ chối thực thi do giới hạn quyền truy cập hoặc cấu hình bảo mật.
[C]
Đường dẫn hoặc tệp tin mà người dùng yêu cầu không tồn tại trên hệ thống máy chủ web.
[EXP]
Tài nguyên không tồn tại trên máy chủ sẽ trả về mã lỗi HTTP `404 Not Found`.
[D]
Máy chủ Nginx gặp lỗi xử lý bên trong hệ thống (Internal Server Error) và không thể hoàn thành yêu cầu.
[EXP]
Lỗi xử lý bên trong máy chủ sẽ trả về mã lỗi HTTP nhóm `5xx`, thường gặp nhất là `500 Internal Server Error`.

@correct: B
@point: 3.3
@difficulty: 5
@concept: nginx-setup
@category: 0

## Q11
Để thêm một tài khoản người dùng thường mới tạo vào nhóm quản trị `sudo` trên hệ điều hành Ubuntu/Linux, lệnh nào dưới đây chính xác và được khuyến nghị sử dụng?

[A]
`sudo useradd -g sudo username`
[EXP]
Tham số `-g` dùng để thay đổi nhóm chính (primary group) mặc định của người dùng thành `sudo`, điều này không đúng quy chuẩn bảo mật phân quyền.
[B]
`sudo groupadd username sudo`
[EXP]
Lệnh `groupadd` dùng để tạo một nhóm mới trên hệ thống, không dùng để thêm người dùng vào một nhóm sẵn có.
[C]
`sudo usermod -aG sudo username`
[EXP]
Đúng. Lệnh `usermod` kết hợp với tùy chọn `-aG` (append to Group) cho phép thêm người dùng vào nhóm phụ `sudo` mà không thay đổi nhóm chính của họ.
[D]
`sudo setuser group=sudo username`
[EXP]
Không tồn tại lệnh nào tên là `setuser` trong tập hợp lệnh quản trị hệ thống Linux tiêu chuẩn.

@correct: C
@point: 3.3
@difficulty: 4
@concept: linux-basics
@category: 0

## Q12
Để cấu hình tường lửa UFW cho phép máy chủ VPS của bạn nhận các yêu cầu truy cập website thông qua giao thức HTTP (cổng 80), lệnh nào dưới đây chính xác?

[A]
`sudo ufw block 80`
[EXP]
Lệnh này chặn kết nối tới cổng 80 chứ không phải cho phép.
[B]
`sudo ufw permit port 80`
[EXP]
Lệnh `ufw` không sử dụng từ khóa `permit` hay `port` trong cấu trúc dòng lệnh của nó.
[C]
`sudo ufw enable 80/tcp`
[EXP]
Lệnh `ufw enable` chỉ dùng để bật tường lửa hoạt động chứ không khai báo thêm luật cho cổng.
[D]
`sudo ufw allow 80/tcp`
[EXP]
Đúng. Lệnh `ufw allow` cho phép mở cổng 80 chạy giao thức TCP nhận traffic từ bên ngoài.

@correct: D
@point: 3.3
@difficulty: 4
@concept: linux-basics
@category: 0

## Q13
Khi cấu hình tính năng HTTP Basic Authentication để bảo mật một thư mục trên website Nginx, tệp tin chứa thông tin username và password mã hóa được tạo ra bởi công cụ nào?

[A]
`htpasswd`
[EXP]
Đúng. Công cụ `htpasswd` (từ gói apache2-utils) được sử dụng để tạo và cập nhật các file lưu trữ thông tin username và mật khẩu đã mã hóa.
[B]
`openssl`
[EXP]
Mặc dù openssl mã hóa được chuỗi ký tự nhưng không tự động sinh cấu trúc định dạng tệp tin cho Nginx auth basic đọc được.
[C]
`ssh-keygen`
[EXP]
Công cụ `ssh-keygen` dùng để tạo cặp khóa SSH, không dùng để sinh mật khẩu truy cập thư mục web tĩnh.
[D]
`passwd`
[EXP]
Lệnh `passwd` dùng để thay đổi mật khẩu hệ điều hành Linux của các tài khoản user, không liên quan đến Nginx basic auth.

@correct: A
@point: 3.3
@difficulty: 5
@concept: nginx-setup
@category: 0

## Q14
Sau khi tiến hành chỉnh sửa nội dung tệp tin cấu hình Nginx trên máy chủ VPS, lệnh hệ thống nào dưới đây giúp Nginx áp dụng cấu hình mới mà không làm gián đoạn các kết nối hiện tại của người dùng?

[A]
`sudo systemctl restart nginx`
[EXP]
Lệnh `restart` sẽ tắt hoàn toàn tiến trình Nginx rồi mới bật lại, gây gián đoạn truy cập của người dùng trong khoảng thời gian đó.
[B]
`sudo systemctl reload nginx`
[EXP]
Đúng. Lệnh `reload` giúp Nginx đọc lại các file cấu hình mới và sinh tiến trình worker mới song song để thay thế tiến trình cũ mà không tắt server.
[C]
`sudo systemctl stop nginx`
[EXP]
Lệnh `stop` tắt hẳn dịch vụ Nginx và không tự khởi động lại để áp dụng cấu hình mới.
[D]
`sudo systemctl enable nginx`
[EXP]
Lệnh `enable` dùng để cấu hình tự động khởi chạy dịch vụ Nginx cùng hệ thống khi boot máy.

@correct: B
@point: 3.3
@difficulty: 4
@concept: nginx-setup
@category: 0

## Q15
Để chỉnh sửa hoặc cấu hình khối Server Block mặc định của web server Nginx trên máy chủ Ubuntu Server, học viên cần tiến hành chỉnh sửa tệp tin nào sau đây?

[A]
`/etc/nginx/nginx.conf.default`
[EXP]
Đây là tệp tin cấu hình mẫu sao lưu dự phòng của hệ thống, không được Nginx load trực tiếp để chạy.
[B]
`/var/www/html/index.nginx-debian.html`
[EXP]
Đây là tệp giao diện HTML tĩnh hiển thị nội dung trang chào mừng mặc định, không chứa các chỉ thị cấu hình hoạt động của web server Nginx.
[C]
`/etc/nginx/sites-available/default`
[EXP]
Đúng. Trên Ubuntu/Debian, tệp `/etc/nginx/sites-available/default` chứa cấu hình server block mặc định lắng nghe cổng 80 của Nginx.
[D]
`/etc/nginx/conf.d/default.conf`
[EXP]
Đường dẫn này thường dùng cho cấu hình mặc định của Nginx cài từ nguồn nginx.org hoặc trên các hệ điều hành RedHat/CentOS, không phải mặc định của Ubuntu.

@correct: C
@point: 3.3
@difficulty: 5
@concept: nginx-setup
@category: 0

## Q16
Kiến trúc lưu trữ của Git bao gồm 3 phân vùng chính. Phân vùng nào lưu trữ các tệp tin mã nguồn vật lý đang được lập trình viên trực tiếp chỉnh sửa trên đĩa cứng máy tính?

[A]
Staging Area
[EXP]
Staging Area là vùng chuẩn bị logic lưu danh sách thay đổi, không phải thư mục vật lý chứa file code đang sửa.
[B]
Git Directory
[EXP]
Git Directory (thư mục ẩn `.git`) là nơi lưu trữ cơ sở dữ liệu lịch sử các commit đã hoàn thành của dự án.
[C]
Remote Repository
[EXP]
Remote Repository là kho chứa lưu trữ trên máy chủ đám mây từ xa (như GitHub) chứ không nằm ở máy local.
[D]
Working Directory
[EXP]
Đúng. Working Directory (Thư mục làm việc) chứa toàn bộ các file dự án hiện tại mà bạn đang trực tiếp sửa đổi.

@correct: D
@point: 3.3
@difficulty: 7
@concept: git-local-basics
@category: 1

## Q17
Khi bạn tạo mới một tệp tin văn bản trong thư mục dự án đã khởi tạo Git, trạng thái mặc định ban đầu của tệp tin này theo nhận diện của Git là gì?

[A]
Untracked
[EXP]
Đúng. File mới tạo hoàn toàn nằm ngoài sự theo dõi của Git nên được xếp vào trạng thái Untracked (Chưa theo dõi).
[B]
Unmodified
[EXP]
File chỉ đạt trạng thái Unmodified sau khi đã được commit và chưa có thay đổi nào mới ở thư mục làm việc.
[C]
Modified
[EXP]
File đạt trạng thái Modified khi nó đã được Git theo dõi từ trước và đang có chỉnh sửa mới chưa đưa vào Staging Area.
[D]
Staged
[EXP]
File đạt trạng thái Staged sau khi học viên chạy lệnh `git add` để đưa file vào vùng chuẩn bị.

@correct: A
@point: 3.3
@difficulty: 7
@concept: git-local-basics
@category: 1

## Q18
Lập trình viên bắt đầu làm việc với Git lần đầu tiên trên một máy tính cá nhân mới. Lệnh nào sau đây được sử dụng để khai báo địa chỉ email của tác giả cho các commit trên phạm vi toàn hệ thống?

[A]
`git config --local user.email "email"`
[EXP]
Tùy chọn `--local` chỉ áp dụng cấu hình email này cho duy nhất repository hiện hành chứ không áp dụng toàn hệ thống.
[B]
`git config --global user.email "email"`
[EXP]
Đúng. Tùy chọn `--global` lưu cấu hình danh tính tác giả áp dụng cho toàn bộ các dự án Git chạy trên máy tính này.
[C]
`git set user.email "email"`
[EXP]
Git không hỗ trợ lệnh bắt đầu bằng từ khóa `git set`.
[D]
`git init user.email "email"`
[EXP]
Lệnh `git init` dùng để khởi tạo repository mới, không dùng để cấu hình thông tin danh tính tác giả.

@correct: B
@point: 3.3
@difficulty: 7
@concept: git-local-basics
@category: 1

## Q19
Để xem danh sách lịch sử các commit đã thực hiện trong dự án dưới dạng rút gọn (mỗi commit nằm trên một dòng hiển thị mã hash ngắn gọn và commit message), bạn sử dụng lệnh nào?

[A]
`git status --short`
[EXP]
Lệnh này hiển thị trạng thái thay đổi hiện tại của các file ở Working Directory và Staging Area dưới dạng rút gọn, không xem lịch sử commit.
[B]
`git show --oneline`
[EXP]
Lệnh `git show` hiển thị chi tiết thay đổi của một commit cụ thể, không liệt kê danh sách lịch sử commit của nhánh.
[C]
`git log --oneline`
[EXP]
Đúng. Tùy chọn `--oneline` định dạng đầu ra của `git log` thành danh sách rút gọn hiển thị mỗi commit trên một dòng.
[D]
`git diff --stat`
[EXP]
Lệnh này so sánh sự khác biệt và thống kê số lượng dòng thay đổi giữa các vùng làm việc, không hiển thị lịch sử commit.

@correct: C
@point: 3.3
@difficulty: 8
@concept: git-advanced-history
@category: 1

## Q20
Trong quá trình gộp nhánh (merge), cơ chế gộp nhanh Fast-Forward được Git tự động áp dụng khi thỏa mãn điều kiện nào sau đây?

[A]
Nhánh hiện tại và nhánh cần gộp có lịch sử commit rẽ nhánh độc lập và có chỉnh sửa trên cùng một dòng code.
[EXP]
Trường hợp này sẽ kích hoạt 3-Way Merge và có khả năng cao dẫn đến xung đột (Merge Conflict).
[B]
Nhánh hiện tại đã có những commit mới phát sinh kể từ khi nhánh cần gộp được tạo ra.
[EXP]
Khi nhánh hiện tại có commit mới, Git bắt buộc phải dùng cơ chế gộp 3 vùng (3-Way Merge) để tạo một commit merge mới.
[C]
Học viên sử dụng tùy chọn `--no-ff` khi thực hiện lệnh gộp nhánh.
[EXP]
Tùy chọn `--no-ff` (no fast-forward) ép buộc Git tạo một commit gộp mới kể cả khi đủ điều kiện chạy fast-forward.
[D]
Nhánh hiện tại chưa có thêm bất kỳ commit mới nào kể từ thời điểm nhánh cần gộp được phân nhánh.
[EXP]
Đúng. Lúc này lịch sử là tuyến tính, Git chỉ cần dịch chuyển con trỏ nhánh hiện tại tiến thẳng lên vị trí commit mới nhất của nhánh cần gộp.

@correct: D
@point: 3.3
@difficulty: 8
@concept: git-branching-conflicts
@category: 1

## Q21
Khi thực hiện gộp nhánh bằng cơ chế 3-Way Merge, Git sẽ tự động sử dụng 3 snapshot nào để so sánh và tạo ra một commit gộp (merge commit) mới?

[A]
Commit mới nhất của nhánh hiện hành, commit mới nhất của nhánh cần gộp, và commit tổ tiên chung gần nhất (Common Ancestor) của hai nhánh.
[EXP]
Đúng. Git đối chiếu 3 điểm này để xác định những thay đổi độc lập của từng nhánh và thực hiện gộp tự động.
[B]
Commit đầu tiên khi khởi tạo dự án, commit mới nhất của nhánh hiện hành, và commit mới nhất của nhánh cần gộp mà học viên chuẩn bị thực hiện.
[EXP]
Commit khởi tạo đầu tiên không phản ánh chính xác điểm phân tách của hai nhánh nên không dùng làm mốc so sánh.
[C]
Ba commit gần đây nhất được thực hiện trên nhánh hiện hành cùng với hai commit bất kỳ được tạo ra trên nhánh cần gộp để làm mốc so sánh.
[EXP]
Git cần so sánh chéo giữa hai nhánh độc lập chứ không chỉ đọc lịch sử của riêng một nhánh hiện tại.
[D]
Commit mới nhất của nhánh hiện hành, commit mới nhất của nhánh cần gộp, và commit mới nhất nằm ở đỉnh của remote repository trên GitHub.
[EXP]
Việc merge local chỉ phụ thuộc vào lịch sử của hai nhánh local và tổ tiên chung của chúng, không liên quan đến đỉnh remote.

@correct: A
@point: 3.3
@difficulty: 9
@concept: git-branching-conflicts
@category: 1

## Q22
Khi xảy ra xung đột gộp nhánh (Merge Conflict), Git sẽ ghi các ký tự đánh dấu xung đột trực tiếp vào file bị lỗi. Ký tự phân tách phần code của nhánh hiện tại (HEAD) và phần code của nhánh cần gộp là gì?

[A]
`<<<<<<<`
[EXP]
Dãy kí tự `<<<<<<<` biểu thị điểm bắt đầu của vùng code xung đột thuộc nhánh hiện hành (HEAD).
[B]
`=======`
[EXP]
Đúng. Dãy ký tự `=======` đóng vai trò vạch phân chia giữa nội dung code của nhánh hiện tại (phía trên) và nhánh cần gộp (phía dưới).
[C]
`>>>>>>>`
[EXP]
Dãy kí tự `>>>>>>>` biểu thị điểm kết thúc của vùng code xung đột thuộc nhánh cần gộp.
[D]
`|||||||`
[EXP]
Dãy ký tự `|||||||` chỉ xuất hiện khi bật chế độ cấu hình hiển thị lịch sử tổ tiên chung (diff3), không phải ký tự phân tách mặc định.

@correct: B
@point: 3.3
@difficulty: 7
@concept: git-branching-conflicts
@category: 1

## Q23
Sau khi học viên đã mở file bị xung đột, thảo luận và chọn lựa giữ lại dòng code chính xác, bước tiếp theo cần thực hiện để hoàn tất quá trình merge nhánh là gì?

[A]
Chạy lệnh `git merge --abort` để lưu lại các chỉnh sửa xung đột vừa thực hiện.
[EXP]
Lệnh `git merge --abort` sẽ hủy bỏ toàn bộ quá trình merge và đưa dự án quay trở lại trạng thái trước khi merge.
[B]
Chạy lệnh `git commit` trực tiếp mà không cần đưa file vào vùng Staging Area.
[EXP]
Git yêu cầu bạn phải đánh dấu file đã giải quyết xung đột bằng lệnh add trước khi cho phép tạo commit merge.
[C]
Chạy lệnh `git add <file>` để đánh dấu đã sửa xung đột, sau đó chạy `git commit` để tạo commit gộp.
[EXP]
Đúng. Thao tác `git add` báo cho Git biết file đã được giải quyết xong xung đột và sẵn sàng tạo commit gộp hoàn thành.
[D]
Chạy lệnh `git push` trực tiếp lên remote repository để máy chủ GitHub tự động sửa lỗi.
[EXP]
Git không cho phép bạn push code lên khi dự án local đang ở trạng thái xung đột chưa được giải quyết xong.

@correct: C
@point: 3.3
@difficulty: 8
@concept: git-branching-conflicts
@category: 1

## Q24
Để thiết lập mối liên kết giữa dự án Git local hiện tại với một repository trống vừa được tạo ra trên GitHub sử dụng giao thức SSH, cú pháp lệnh nào sau đây chính xác?

[A]
`git remote add git@github.com:username/repo.git`
[EXP]
Lệnh này thiếu tên định danh (alias) cho remote repository ở máy local (thường là `origin`).
[B]
`git remote origin add git@github.com:username/repo.git`
[EXP]
Tên định danh `origin` phải được đặt sau từ khóa hành động `add` trong cấu trúc lệnh.
[C]
`git remote add link git@github.com:username/repo.git`
[EXP]
Mặc dù cú pháp này đúng nhưng tên định danh là `link`, không tuân theo tiêu chuẩn mặc định thông dụng của Git.
[D]
`git remote add origin git@github.com:username/repo.git`
[EXP]
Đúng. Lệnh khai báo liên kết remote có bí danh là `origin` trỏ tới đường dẫn URL dạng SSH của GitHub.

@correct: D
@point: 3.3
@difficulty: 8
@concept: git-remote-github
@category: 1

## Q25
Để cấu hình xác thực SSH thành công với tài khoản GitHub cá nhân, học viên cần truy cập vào mục **Settings -> SSH and GPG keys** trên giao diện web của GitHub và thực hiện dán nội dung của tệp tin nào?

[A]
`~/.ssh/id_ed25519.pub`
[EXP]
Đúng. Bạn phải dán nội dung khóa công khai (Public Key - đuôi `.pub`) của máy local lên GitHub Console để xác thực.
[B]
`~/.ssh/id_ed25519`
[EXP]
Đây là khóa riêng tư (Private Key), cần giữ bí mật tuyệt đối trên máy local và không bao giờ được upload hay chia sẻ.
[C]
`~/.ssh/known_hosts`
[EXP]
Tệp này lưu fingerprint nhận diện các host server ngoài hệ thống, không phải khóa xác thực của bạn.
[D]
`~/.ssh/config`
[EXP]
Tệp này dùng để định cấu hình các kết nối SSH ở local, không chứa khóa mã hóa xác thực dán lên GitHub.

@correct: A
@point: 3.3
@difficulty: 7
@concept: git-remote-github
@category: 1

## Q26
Khi chạy lệnh `git push`, học viên bị GitHub từ chối (rejected - non-fast-forward) vì remote repository đã có những commit mới do thành viên khác đẩy lên trước. Lệnh nào giúp kéo và gộp an toàn các thay đổi đó về local trước khi push lại?

[A]
`git push -f`
[EXP]
Lệnh push force sẽ ghi đè thô bạo lên remote, xóa sạch lịch sử commit của thành viên kia, gây mất code nghiêm trọng.
[B]
`git pull`
[EXP]
Đúng. Lệnh `git pull` tải các thay đổi mới nhất từ remote về và tự động tiến hành gộp (merge) vào nhánh local hiện tại để đồng bộ.
[C]
`git clone`
[EXP]
Lệnh `git clone` chỉ dùng để tải dự án về lần đầu tiên khi local chưa có mã nguồn, không dùng để đồng bộ lịch sử.
[D]
`git init`
[EXP]
Lệnh `git init` dùng để khởi tạo một repository trống tại local, không có chức năng đồng bộ dữ liệu mạng.

@correct: B
@point: 3.3
@difficulty: 9
@concept: git-remote-github
@category: 1

## Q27
Học viên lỡ gõ sai thông điệp commit vừa tạo ở local và muốn sửa đổi ngay lập tức mà không muốn lịch sử dự án xuất hiện thêm một commit sửa đổi rác. Lệnh nào hỗ trợ giải quyết yêu cầu này?

[A]
`git commit -m "tin_nhan_moi"`
[EXP]
Lệnh này sẽ tạo thêm một commit hoàn toàn mới kế tiếp, khiến lịch sử xuất hiện commit thừa không đáng có.
[B]
`git reset --hard HEAD`
[EXP]
Lệnh này xóa bỏ hoàn toàn commit gần nhất và xóa sạch các code đã viết, không phải lệnh sửa thông điệp.
[C]
`git commit --amend -m "tin_nhan_moi"`
[EXP]
Đúng. Tùy chọn `--amend` cho phép ghi đè nội dung và sửa đổi thông điệp của commit gần nhất ở nhánh hiện tại.
[D]
`git revert HEAD`
[EXP]
Lệnh revert tạo ra một commit mới để đảo ngược thay đổi của commit cũ, không dùng để sửa tin nhắn commit.

@correct: C
@point: 3.3
@difficulty: 8
@concept: git-advanced-history
@category: 1

## Q28
Tùy chọn nào dưới đây của lệnh `git reset` sẽ di chuyển con trỏ nhánh lùi về quá khứ đồng thời xóa sạch toàn bộ các thay đổi ở cả Staging Area và Working Directory (khiến mã nguồn bị hủy bỏ triệt để)?

[A]
`--soft`
[EXP]
Tùy chọn `--soft` giữ nguyên các file thay đổi tại vùng đệm Staging Area để người dùng sẵn sàng commit lại.
[B]
`--mixed`
[EXP]
Tùy chọn `--mixed` xóa Staging Area nhưng vẫn giữ lại toàn bộ code thay đổi tại thư mục làm việc Working Directory.
[C]
`--keep`
[EXP]
Tùy chọn `--keep` dời con trỏ nhánh nhưng giữ lại các thay đổi local chưa commit nếu không gây xung đột, không xóa sạch mọi thứ.
[D]
`--hard`
[EXP]
Đúng. Chế độ `--hard` là chế độ reset mạnh nhất, dọn sạch toàn bộ thay đổi ở cả 3 vùng làm việc.

@correct: D
@point: 3.3
@difficulty: 9
@concept: git-advanced-history
@category: 1

## Q29
Khi làm việc nhóm trên nhánh chính `main` đã được đẩy lên remote, cách thức an toàn nhất để hủy bỏ thay đổi của một commit lỗi trong quá khứ mà không gây xung đột lịch sử cho các thành viên khác là gì?

[A]
Chạy lệnh `git revert <commit_hash>` để tạo một commit mới đảo ngược các thay đổi lỗi.
[EXP]
Đúng. `git revert` tạo commit mới đi tiếp lịch sử giúp tránh việc viết lại lịch sử commit trên remote gây lỗi cho nhóm.
[B]
Chạy lệnh `git reset --hard <commit_hash>` rồi chạy `git push -f` lên remote.
[EXP]
Việc reset và push force viết lại lịch sử nhánh chung sẽ làm lệch lịch sử làm việc của mọi thành viên khác và gây lỗi nghiêm trọng.
[C]
Xóa thủ công tệp tin bị lỗi trực tiếp trên giao diện website GitHub Console.
[EXP]
Việc xóa trực tiếp trên web vẫn tạo ra commit mới lệch với local, và không giải quyết tận gốc vấn đề đồng bộ lịch sử của nhóm.
[D]
Chạy lệnh `git branch -D main` để xóa nhánh chính và tạo lại nhánh mới từ đầu.
[EXP]
Xóa nhánh chính sẽ hủy hoại toàn bộ lịch sử dự án và làm đứt gãy quy trình teamwork của nhóm.

@correct: A
@point: 3.3
@difficulty: 8
@concept: git-advanced-history
@category: 1

## Q30
Học viên muốn sao chép duy nhất một commit sửa lỗi hotfix (ví dụ commit `C8`) từ nhánh phát triển `feature` sang nhánh chính `main` mà không muốn gộp toàn bộ các commit thử nghiệm khác trên nhánh `feature`. Lệnh nào đáp ứng?

[A]
`git merge feature`
[EXP]
Lệnh merge sẽ gộp toàn bộ lịch sử và tất cả các commit của nhánh `feature` vào `main`, không chọn lọc được riêng commit `C8`.
[B]
`git cherry-pick <commit_hash_C8>`
[EXP]
Đúng. Lệnh `git cherry-pick` cho phép trích xuất chính xác một commit cụ thể dựa trên mã băm của nó áp dụng lên nhánh hiện tại.
[C]
`git checkout feature <commit_hash_C8>`
[EXP]
Cú pháp này không hợp lệ trong Git khi muốn sao chép commit giữa các nhánh làm việc.
[D]
`git reset --soft <commit_hash_C8>`
[EXP]
Lệnh reset dùng để dịch chuyển lịch sử của nhánh hiện hành chứ không dùng để sao chép commit từ nhánh phụ sang.

@correct: B
@point: 3.3
@difficulty: 9
@concept: git-advanced-history
@category: 1
