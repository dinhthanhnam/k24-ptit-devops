---
schema_version: 1
id: ss02_quiz_warm_up
type: quiz
status: draft
course_id: devops-basic
session: 2
unit: 0
title: Quiz đầu giờ Session 02
session_kind: theory
tags: []
concepts: []
depends_on:
- ss02_lesson_01
- ss02_lesson_02
- ss02_lesson_03
- ss02_lesson_04
builds_on: []
enables: []
owns: []
assumes: []
does_not_cover:
- vps-deploy
source: generated
pm_ref: Session 02 / quiz_warm_up
language: vi
created: '2026-07-15'
updated: '2026-07-15'
quiz_kind: warm_up
question_count: 30
maps_to:
- ss02_lesson_01
- ss02_lesson_02
- ss02_lesson_03
- ss02_lesson_04
---

# Quiz đầu giờ Session 02

## Q1
Thuật ngữ "DevOps" được ghép lại từ hai bộ phận chức năng nào trong quy trình phần mềm?

[A]
Bộ phận phát triển (Development) và bộ phận vận hành (Operations).
[EXP]
Đúng. DevOps là sự kết hợp của Development và Operations nhằm tối ưu quy trình bàn giao.
[B]
Bộ phận thiết kế (Design) và bộ phận tối ưu hóa (Optimization).
[EXP]
Sai. Đây không phải là nguồn gốc hình thành khái niệm DevOps.
[C]
Bộ phận phát triển (Development) và bộ phận cơ sở dữ liệu (Database).
[EXP]
Sai. Cơ sở dữ liệu chỉ là một phần nhỏ của vận hành, không phải từ gốc Ops.
[D]
Bộ phận bảo mật (Security) và bộ phận kiểm thử (Testing).
[EXP]
Sai. Bảo mật thường viết tắt là Sec trong DevSecOps, không nằm trong từ DevOps.

@correct: A
@point: 20
@difficulty: 4
@concept: devops-introduction
@category: 0

## Q2
Trong mô hình làm việc truyền thống, "Bức tường hoang mang" (Wall of Confusion) xuất hiện do đâu?

[A]
Do sự bất đồng về múi giờ làm việc giữa Dev và Ops.
[EXP]
Sai. Sự khác biệt múi giờ chỉ là vấn đề địa lý, không phải bản chất của Wall of Confusion.
[B]
Do mục tiêu đối lập giữa Dev (muốn nhanh) và Ops (muốn ổn định).
[EXP]
Đúng. Dev muốn liên tục cập nhật tính năng mới, còn Ops muốn hệ thống hoạt động ổn định nhất nên e ngại thay đổi.
[C]
Do không có chung ngôn ngữ lập trình giữa lập trình viên và quản trị viên.
[EXP]
Sai. DevOps không bắt buộc Dev và Ops phải dùng chung một ngôn ngữ lập trình.
[D]
Do các nhà quản lý dự án không cung cấp đủ tài liệu kỹ thuật phần cứng.
[EXP]
Sai. Thiếu tài liệu chỉ là lỗi quy trình nhỏ, không đại diện cho Wall of Confusion.

@correct: B
@point: 20
@difficulty: 4
@concept: devops-introduction
@category: 0

## Q3
Biểu tượng vòng lặp vô cực (infinity loop) trong DevOps thể hiện tính chất nào sau đây?

[A]
Quy trình phần mềm bị lặp lỗi liên tục không có điểm dừng.
[EXP]
Sai. Quy trình không hướng tới việc lặp lỗi mà hướng tới sự ổn định cải tiến liên tục.
[B]
Chi phí vận hành dự án sẽ tăng lên vô hạn theo thời gian.
[EXP]
Sai. DevOps giúp tối ưu hóa và giảm chi phí dài hạn chứ không tăng vô hạn.
[C]
Mối liên kết chặt chẽ và phản hồi liên tục giữa Dev và Ops.
[EXP]
Đúng. Biểu tượng vô cực thể hiện chu kỳ khép kín phản hồi liên tục từ lập kế hoạch tới vận hành giám sát.
[D]
Thời gian triển khai một tính năng sẽ kéo dài mãi mãi.
[EXP]
Sai. DevOps nhằm mục tiêu rút ngắn tối đa thời gian phát hành tính năng.

@correct: C
@point: 20
@difficulty: 4
@concept: devops-introduction
@category: 0

## Q4
Trong các giai đoạn của vòng lặp DevOps, hoạt động "Build" trực tiếp thực hiện nhiệm vụ gì?

[A]
Thiết kế giao diện người dùng và trải nghiệm khách hàng.
[EXP]
Sai. Thiết kế giao diện thuộc giai đoạn lập kế hoạch (Plan) hoặc thiết kế, không thuộc Build.
[B]
Lắng nghe phản hồi từ khách hàng để cải tiến sản phẩm.
[EXP]
Sai. Phản hồi khách hàng nằm ở giai đoạn giám sát và vận hành (Monitor/Operate).
[C]
Kiểm thử tự động mã nguồn để phát hiện các lỗi bảo mật.
[EXP]
Sai. Kiểm thử tự động thuộc giai đoạn Test, diễn ra sau hoặc song song với Build.
[D]
Biên dịch mã nguồn thô và đóng gói thành tệp tin chạy được.
[EXP]
Đúng. Giai đoạn Build thực hiện biên dịch mã nguồn và đóng gói sản phẩm (ví dụ đóng gói file JAR, WAR).

@correct: D
@point: 20
@difficulty: 4
@concept: devops-introduction
@category: 0

## Q5
Giai đoạn nào trong vòng lặp DevOps chịu trách nhiệm đưa ứng dụng đã đóng gói lên máy chủ chạy thực tế?

[A]
Giai đoạn triển khai (Deploy).
[EXP]
Đúng. Deploy là bước chuyển giao và cài đặt ứng dụng lên các môi trường máy chủ như Cloud hoặc VPS.
[B]
Giai đoạn lập kế hoạch (Plan).
[EXP]
Sai. Giai đoạn Plan chỉ diễn ra ở đầu chu kỳ để thiết lập các yêu cầu phần mềm.
[C]
Giai đoạn viết mã (Code).
[EXP]
Sai. Giai đoạn Code chỉ liên quan đến lập trình viên viết logic phần mềm trên máy cá nhân.
[D]
Giai đoạn kiểm thử (Test).
[EXP]
Sai. Giai đoạn Test dùng để phát hiện lỗi sản phẩm trước khi mang đi triển khai.

@correct: A
@point: 20
@difficulty: 4
@concept: devops-introduction
@category: 0

## Q6
Khi một nhóm nói rằng họ đã áp dụng thành công DevOps chỉ bằng cách cài đặt công cụ Docker, nhận định nào sau đây là chính xác?

[A]
Họ đã đạt DevOps vì Docker là công cụ duy nhất cần thiết.
[EXP]
Sai. Không có một công cụ đơn lẻ nào giúp đạt được DevOps hoàn chỉnh.
[B]
Họ mới chỉ áp dụng công cụ, chưa thay đổi văn hóa và quy trình.
[EXP]
Đúng. DevOps đòi hỏi sự thay đổi đồng bộ cả văn hóa phối hợp Dev-Ops và quy trình làm việc chứ không chỉ cài đặt công cụ.
[C]
Họ đã hoàn thành 90% khối lượng công việc của DevOps.
[EXP]
Sai. Cài đặt Docker chỉ là một phần kỹ thuật nhỏ trong toàn bộ vòng đời DevOps.
[D]
Họ đang đi sai hướng hoàn toàn vì Docker không liên quan đến DevOps.
[EXP]
Sai. Docker là công cụ bổ trợ rất tốt cho DevOps, nhưng chỉ dùng Docker thì chưa đủ để gọi là DevOps.

@correct: B
@point: 20
@difficulty: 4
@concept: devops-introduction
@category: 0

## Q7
Mục tiêu cốt lõi của hoạt động giám sát (Monitor) trong chu kỳ DevOps là gì?

[A]
Theo dõi thời gian làm việc hàng ngày của lập trình viên.
[EXP]
Sai. Monitor hướng tới giám sát hệ thống kỹ thuật và ứng dụng, không phải kiểm soát thời gian nhân sự.
[B]
Ngăn chặn hoàn toàn lập trình viên chỉnh sửa mã nguồn.
[EXP]
Sai. DevOps khuyến khích cập nhật liên tục chứ không ngăn chặn Dev sửa mã nguồn.
[C]
Thu thập dữ liệu hiệu năng hệ thống để phát hiện và xử lý lỗi sớm.
[EXP]
Đúng. Monitor giúp thu thập thông số CPU, RAM, Log hệ thống để kịp thời cảnh báo sự cố trước khi người dùng phát hiện.
[D]
Tự động xóa các máy ảo đang chạy quá tải để giảm chi phí.
[EXP]
Sai. Việc tự động xóa máy chủ quá tải có thể làm gián đoạn dịch vụ, không phải mục đích giám sát.

@correct: C
@point: 20
@difficulty: 5
@concept: devops-introduction
@category: 0

## Q8
Lý do tại sao việc tự động hóa (Automation) lại được coi là xương sống của quy trình DevOps?

[A]
Tự động hóa giúp loại bỏ hoàn toàn vai trò của lập trình viên.
[EXP]
Sai. Lập trình viên vẫn cần thiết để viết logic ứng dụng và thiết kế hệ thống.
[B]
Tự động hóa giúp tiết kiệm 100% chi phí mua phần cứng máy chủ.
[EXP]
Sai. Phần cứng vẫn phải mua hoặc thuê trên Cloud, tự động hóa không làm biến mất phần cứng vật lý.
[C]
Tự động hóa chỉ áp dụng cho việc gửi email báo cáo tiến độ.
[EXP]
Sai. Tự động hóa áp dụng cho toàn chu kỳ từ build, test đến deploy.
[D]
Tự động hóa giúp giảm thiểu lỗi con người và tăng tốc độ bàn giao.
[EXP]
Đúng. Các thao tác thủ công dễ gây ra nhầm lẫn, tự động hóa đảm bảo quy trình chạy nhất quán và nhanh chóng.

@correct: D
@point: 20
@difficulty: 5
@concept: devops-introduction
@category: 0

## Q9
Trong khóa học DevOps Basics, công cụ nào sau đây được giới thiệu để thực hiện vai trò máy chủ Web trung gian phục vụ ứng dụng?

[A]
Web Server Nginx.
[EXP]
Đúng. Nginx được giới thiệu ở Session 2 để đóng vai trò làm Web Server và Reverse Proxy phục vụ các trang tĩnh/động.
[B]
Hệ điều hành Windows.
[EXP]
Sai. Windows là hệ điều hành máy tính cá nhân/máy chủ, không phải Web Server chuyên dụng trong bài học.
[C]
Công cụ quản lý Git.
[EXP]
Sai. Git là công cụ quản trị phiên bản mã nguồn, không có tính năng phục vụ Web.
[D]
Hệ thống giám sát Grafana.
[EXP]
Sai. Grafana là công cụ trực quan hóa dữ liệu giám sát, không phải Web Server.

@correct: A
@point: 20
@difficulty: 5
@concept: devops-introduction
@category: 0

## Q10
Điểm khác biệt lớn nhất giữa việc học DevOps lý thuyết và thực hành thực chiến là gì?

[A]
Lý thuyết chỉ học về các mô hình toán học phức tạp.
[EXP]
Sai. Lý thuyết DevOps chủ yếu học về quy trình và văn hóa làm việc, không liên quan đến toán học phức tạp.
[B]
Thực hành yêu cầu tự tay thiết lập, cấu hình phần mềm và gỡ lỗi.
[EXP]
Đúng. Kỹ năng DevOps chỉ có thể đạt được khi học viên tự tay gõ lệnh, cấu hình dịch vụ và tự debug các lỗi phát sinh.
[C]
Học lý thuyết giúp hệ thống tự động chạy mà không cần gõ lệnh.
[EXP]
Sai. Học lý thuyết không thể giúp hệ thống hoạt động thực tế nếu không cài đặt.
[D]
Thực hành chỉ dành cho các chuyên gia có trên 10 năm kinh nghiệm.
[EXP]
Sai. Bất kỳ ai bắt đầu học DevOps đều phải thực hành các bài lab cơ bản như khởi tạo VPS hay cấu hình Nginx.

@correct: B
@point: 20
@difficulty: 5
@concept: devops-introduction
@category: 0

## Q11
Khi áp dụng DevOps, sự phối hợp giữa Dev và Ops được cải thiện chủ yếu thông qua yếu tố văn hóa nào?

[A]
Dev và Ops phải hoạt động hoàn toàn độc lập và không can thiệp nhau.
[EXP]
Sai. Hoạt động độc lập chính là mô hình Silo cũ cần xóa bỏ.
[B]
Lập trình viên chịu trách nhiệm gánh vác toàn bộ công việc của Ops.
[EXP]
Sai. Đây là sự đùn đẩy công việc, không phải phối hợp đồng hành.
[C]
Chia sẻ trách nhiệm chung về chất lượng sản phẩm và sự ổn định.
[EXP]
Đúng. Cả hai bộ phận cùng tham gia vào quá trình thiết kế, triển khai và theo dõi ứng dụng để nhanh chóng giải quyết sự cố.
[D]
Ops chỉ thực hiện nhiệm vụ khi Dev viết xong tài liệu dài 100 trang.
[EXP]
Sai. Tài liệu quá dài làm chậm quy trình bàn giao, đi ngược lại tinh thần Agile/DevOps.

@correct: C
@point: 20
@difficulty: 5
@concept: devops-introduction
@category: 0

## Q12
Một doanh nghiệp muốn giảm thời gian từ khi hoàn thành viết mã đến khi ứng dụng chạy trên internet từ 2 tuần xuống còn 10 phút. Giải pháp DevOps nào là phù hợp nhất?

[A]
Thuê thêm thật nhiều nhân sự kiểm thử phần mềm thủ công.
[EXP]
Sai. Kiểm thử thủ công tốn nhiều thời gian và dễ bỏ sót lỗi, khó đạt mốc 10 phút.
[B]
Yêu cầu lập trình viên không được tạo thêm nhánh code mới.
[EXP]
Sai. Không tạo nhánh code mới sẽ bóp nghẹt khả năng phát triển tính năng song song.
[C]
Chỉ cho phép ứng dụng chạy trên máy tính cá nhân của lập trình viên.
[EXP]
Sai. Ứng dụng phải đưa lên môi trường sản xuất để phục vụ người dùng thực tế.
[D]
Xây dựng đường ống tự động hóa kiểm thử và triển khai (CI/CD pipeline).
[EXP]
Đúng. CI/CD pipeline tự động hóa toàn bộ chu kỳ tích hợp và triển khai giúp đưa code lên server an toàn chỉ trong vài phút.

@correct: D
@point: 20
@difficulty: 6
@concept: devops-introduction
@category: 0

## Q13
Tại sao trong lộ trình học DevOps, Git/GitHub lại là nhóm kỹ năng được ưu tiên học ngay sau phần hạ tầng cơ bản?

[A]
Vì Git giúp lưu trữ mã nguồn và là điểm khởi đầu của mọi quy trình tự động hóa.
[EXP]
Đúng. Mã nguồn được quản lý tốt trên Git mới có thể kích hoạt các trigger tự động biên dịch, đóng gói và triển khai.
[B]
Vì Git là công cụ duy nhất dùng để cài đặt hệ điều hành lên VPS.
[EXP]
Sai. Git không dùng để cài đặt hệ điều hành lên VPS.
[C]
Vì sử dụng Git sẽ giúp tự động sửa toàn bộ các lỗi cú pháp code.
[EXP]
Sai. Git chỉ lưu trữ lịch sử thay đổi mã nguồn, không tự động sửa lỗi logic của lập trình viên.
[D]
Vì GitHub là mạng xã hội duy nhất dành cho các kỹ sư vận hành.
[EXP]
Sai. GitHub là nền tảng quản lý mã nguồn, không phải mạng xã hội đơn thuần cho Ops.

@correct: A
@point: 20
@difficulty: 6
@concept: devops-introduction
@category: 0

## Q14
Vai trò của việc đóng gói ứng dụng (ví dụ sử dụng Docker) trong quy trình DevOps là gì?

[A]
Đảm bảo ứng dụng chạy giống hệt nhau trên mọi môi trường phát triển và vận hành.
[EXP]
Đúng. Đóng gói giúp gom ứng dụng kèm theo toàn bộ thư viện phụ thuộc, giải quyết triệt để lỗi "chạy được trên máy tôi nhưng lỗi trên server".
[B]
Tự động tăng tốc độ xử lý tính toán của ứng dụng lên gấp 10 lần.
[EXP]
Sai. Đóng gói không can thiệp tối ưu hiệu suất giải thuật của mã nguồn.
[C]
Thay thế hoàn toàn sự cần thiết của hệ điều hành trên máy chủ vật lý.
[EXP]
Sai. Ứng dụng đóng gói vẫn cần chạy trên một hệ điều hành Host bên dưới.
[D]
Giúp lập trình viên không cần phải viết code logic cho ứng dụng nữa.
[EXP]
Sai. Docker chỉ đóng gói sản phẩm, lập trình viên vẫn phải viết mã nguồn bình thường.

@correct: B
@point: 20
@difficulty: 6
@concept: devops-introduction
@category: 0

## Q15
Ý nghĩa của việc tích hợp Prometheus và Grafana vào lộ trình học tập DevOps là gì?

[A]
Để tự động biên dịch mã nguồn Java thành các file chạy độc lập.
[EXP]
Sai. Việc biên dịch ứng dụng Java do Maven/Gradle đảm nhận, không phải Prometheus/Grafana.
[B]
Cung cấp khả năng theo dõi trạng thái sức khỏe hệ thống qua biểu đồ trực quan.
[EXP]
Đúng. Prometheus thu thập số liệu (metrics) hiệu năng còn Grafana vẽ biểu đồ, giúp Ops giám sát và phát hiện sự cố sớm.
[C]
Để thay thế hoàn toàn tường lửa UFW trong việc bảo mật máy chủ.
[EXP]
Sai. Prometheus và Grafana không có tính năng lọc gói tin bảo mật như tường lửa.
[D]
Để tự động tạo khóa SSH Key mỗi khi có tài khoản mới đăng nhập.
[EXP]
Sai. Tạo khóa SSH do lệnh ssh-keygen đảm nhận.

@correct: C
@point: 20
@difficulty: 6
@concept: devops-introduction
@category: 0

## Q16
Ý nghĩa cốt lõi của công nghệ ảo hóa (Virtualization) trong kỷ nguyên điện toán đám mây là gì?

[A]
Loại bỏ hoàn toàn sự cần thiết của các thiết bị phần cứng vật lý trong trung tâm dữ liệu.
[EXP]
Sai. Ảo hóa vẫn chạy trên hạ tầng phần cứng thực tế, không thể loại bỏ thiết bị vật lý.
[B]
Tăng tốc độ kết nối internet vật lý của các đường truyền cáp quang.
[EXP]
Sai. Ảo hóa không tác động đến cơ sở hạ tầng mạng cáp quang vật lý.
[C]
Chuyển đổi giao diện ứng dụng từ dạng văn bản dòng lệnh sang dạng đồ họa 3D.
[EXP]
Sai. Đây là công nghệ kết xuất đồ họa, không phải ảo hóa tài nguyên.
[D]
Trừu tượng hóa và chia sẻ tài nguyên phần cứng vật lý thành nhiều môi trường ảo cô lập.
[EXP]
Đúng. Ảo hóa giúp tạo ra các máy ảo hoạt động độc lập nhằm tối ưu hóa hiệu suất khai thác phần cứng.

@correct: D
@point: 20
@difficulty: 7
@concept: virtualization-basics
@category: 1

## Q17
Thành phần Hypervisor trong kiến trúc ảo hóa đóng vai trò gì?

[A]
Quản lý, phân phối tài nguyên phần cứng và đảm bảo tính cô lập giữa các máy ảo.
[EXP]
Đúng. Hypervisor (VMM) kiểm soát tài nguyên CPU, RAM, Disk vật lý để cấp phát an toàn cho từng VM.
[B]
Là hệ điều hành duy nhất được phép cài đặt bên trong các máy ảo Guest OS.
[EXP]
Sai. Bên trong máy ảo có thể cài đặt nhiều hệ điều hành khác nhau như Ubuntu, CentOS, Windows.
[C]
Dịch toàn bộ mã nguồn của lập trình viên sang ngôn ngữ máy để chạy ứng dụng.
[EXP]
Sai. Nhiệm vụ dịch mã nguồn là của trình biên dịch (compiler), không phải Hypervisor.
[D]
Quét virus và mã độc tự động cho các máy tính cá nhân của học viên.
[EXP]
Sai. Đây là chức năng của phần mềm diệt virus (Antivirus).

@correct: A
@point: 20
@difficulty: 7
@concept: virtualization-basics
@category: 1

## Q18
Một máy chủ ảo VPS (Virtual Private Server) được khởi tạo bằng công nghệ ảo hóa có đặc điểm nào sau đây?

[A]
Phải sử dụng chung hệ điều hành và tệp tin cấu hình với máy chủ vật lý Host.
[EXP]
Sai. Mỗi VPS chạy một hệ điều hành khách (Guest OS) hoàn toàn độc lập với Host OS.
[B]
Có hệ điều hành, tài nguyên cấu hình (CPU, RAM, Disk) và địa chỉ IP riêng biệt.
[EXP]
Đúng. VPS hoạt động như một máy tính độc lập giúp đảm bảo tính cô lập và an toàn.
[C]
Tự động biến mất và xóa sạch dữ liệu mỗi khi người dùng ngắt phiên kết nối SSH.
[EXP]
Sai. VPS lưu trữ dữ liệu bền vững trên ổ đĩa ảo, không bị xóa khi tắt kết nối SSH.
[D]
Chỉ chạy được các ứng dụng dòng lệnh cơ bản và không kết nối được internet.
[EXP]
Sai. VPS có thể kết nối internet qua IP Public và chạy mọi loại dịch vụ dịch vụ phức tạp.

@correct: B
@point: 20
@difficulty: 7
@concept: cloud-server-provisioning
@category: 1

## Q19
Khi chọn vị trí đặt máy chủ ảo (Region) cho ứng dụng phục vụ người dùng tại Việt Nam, tại sao nên ưu tiên chọn Singapore?

[A]
Vì chi phí thuê máy chủ tại khu vực Singapore luôn rẻ bằng một nửa so với Mỹ.
[EXP]
Sai. Chi phí thuê VPS phụ thuộc vào cấu hình và nhà cung cấp, không phải do Region rẻ hơn một nửa.
[B]
Vì chỉ có Region Singapore mới hỗ trợ cài đặt máy chủ Web Nginx.
[EXP]
Sai. Mọi Region của các nhà cung cấp cloud đều hỗ trợ cài đặt Nginx.
[C]
Vì khoảng cách địa lý gần giúp giảm thiểu độ trễ đường truyền mạng vật lý.
[EXP]
Đúng. Khoảng cách địa lý gần giúp tín hiệu truyền nhanh hơn, giảm độ trễ (latency) cho người dùng cuối.
[D]
Vì luật pháp bắt buộc mọi học viên PTIT phải đặt máy chủ ở Đông Nam Á.
[EXP]
Sai. Việc chọn hoàn toàn dựa trên tối ưu hóa kỹ thuật đường truyền, không có luật pháp bắt buộc.

@correct: C
@point: 20
@difficulty: 7
@concept: cloud-server-provisioning
@category: 1

## Q20
Điểm khác biệt cốt lõi giữa Hypervisor Type 1 (Bare-metal) và Hypervisor Type 2 (Hosted) là gì?

[A]
Type 1 cài trên Windows còn Type 2 cài trực tiếp trên máy chủ vật lý.
[EXP]
Sai. Ngược lại, Type 1 cài trực tiếp phần cứng còn Type 2 phải chạy qua hệ điều hành Host.
[B]
Type 1 chỉ chạy được máy ảo Linux còn Type 2 chỉ chạy được máy ảo Windows.
[EXP]
Sai. Cả hai loại đều hỗ trợ đa dạng hệ điều hành khách (Guest OS).
[C]
Type 2 hoàn toàn miễn phí còn Type 1 bắt buộc phải mua bản quyền đắt tiền.
[EXP]
Sai. Cả hai loại đều có các giải pháp miễn phí/mã nguồn mở hoặc trả phí tương ứng.
[D]
Type 1 chạy trực tiếp trên phần cứng vật lý còn Type 2 chạy trên một hệ điều hành Host.
[EXP]
Đúng. Do chạy trực tiếp nên Type 1 mang lại hiệu năng cao và độ trễ thấp hơn hẳn so với Type 2.

@correct: D
@point: 20
@difficulty: 7
@concept: virtualization-basics
@category: 1

## Q21
Mục đích của việc sử dụng cặp khóa SSH Key (thuật toán Ed25519) thay thế cho mật khẩu truyền thống là gì?

[A]
Tăng mức độ bảo mật, chống các cuộc tấn công dò quét mật khẩu tự động (Brute-force).
[EXP]
Đúng. Xác thực khóa SSH dựa trên mật mã khóa công khai rất khó bị bẻ khóa so với mật khẩu thông thường.
[B]
Giúp giảm dung lượng bộ nhớ RAM tiêu thụ của ứng dụng khi chạy trên máy chủ.
[EXP]
Sai. SSH Key chỉ phục vụ xác thực kết nối, không ảnh hưởng đến RAM tiêu thụ của ứng dụng.
[C]
Tự động tăng tốc độ xử lý các truy vấn cơ sở dữ liệu trên VPS.
[EXP]
Sai. SSH Key không liên quan đến hiệu suất cơ sở dữ liệu.
[D]
Ngăn chặn hoàn toàn Nginx ghi nhận nhật ký log của hệ điều hành.
[EXP]
Sai. Nginx ghi log độc lập với phương thức xác thực SSH của máy chủ.

@correct: A
@point: 20
@difficulty: 7
@concept: cloud-server-provisioning
@category: 1

## Q22
Lệnh nào sau đây được sử dụng để tạo cặp khóa SSH mới trên máy tính cá nhân sử dụng thuật toán Ed25519?

[A]
`cat ~/.ssh/id_ed25519.pub`
[EXP]
Sai. Lệnh này dùng để đọc và hiển thị nội dung khóa công khai đã có sẵn.
[B]
`ssh-keygen -t ed25519 -C "email@example.com"`
[EXP]
Đúng. Tham số `-t ed25519` yêu cầu trình tạo khóa tạo ra cặp khóa sử dụng thuật toán hiện đại Ed25519.
[C]
`ssh root@<IP_ADDRESS>`
[EXP]
Sai. Đây là lệnh để thực hiện kết nối SSH tới máy chủ từ xa, không phải tạo khóa.
[D]
`sudo systemctl restart ssh`
[EXP]
Sai. Đây là lệnh khởi động lại dịch vụ SSH daemon trên máy chủ ảo Linux.

@correct: B
@point: 20
@difficulty: 8
@concept: cloud-server-provisioning
@category: 1

## Q23
Trong cấu hình phân quyền sudo của Linux, chỉ thị `sys-viewer ALL=(root) NOPASSWD: /usr/bin/cat /var/log/nginx/*` có ý nghĩa gì?

[A]
Cho phép user `sys-viewer` chạy mọi lệnh hệ thống dưới quyền root mà không cần mật khẩu.
[EXP]
Sai. Lệnh bị giới hạn rõ ràng chỉ được chạy `/usr/bin/cat /var/log/nginx/*`.
[B]
Cấm user `sys-viewer` sử dụng lệnh `cat` trên toàn bộ hệ thống máy chủ.
[EXP]
Sai. Lệnh này cấp quyền chạy `cat` cho các file log Nginx chứ không cấm.
[C]
Cho phép user `sys-viewer` chạy lệnh `cat` xem file log Nginx với quyền root mà không cần nhập mật khẩu.
[EXP]
Đúng. Từ khóa `NOPASSWD` kết hợp với đường dẫn lệnh cụ thể cho phép chạy lệnh đó qua sudo không cần mật khẩu.
[D]
Yêu cầu user `sys-viewer` phải nhập mật khẩu root mỗi khi muốn xem nhật ký log.
[EXP]
Sai. `NOPASSWD` nghĩa là không yêu cầu nhập mật khẩu khi chạy lệnh được định nghĩa.

@correct: C
@point: 20
@difficulty: 8
@concept: infrastructure-security
@category: 1

## Q24
Để chỉnh sửa cấu hình phân quyền sudoers một cách an toàn tránh làm hỏng file gây khóa hệ thống, lệnh nào được khuyến nghị sử dụng?

[A]
`sudo nano /etc/sudoers`
[EXP]
Sai. Dùng nano sửa trực tiếp file gốc không có cơ chế kiểm tra lỗi cú pháp trước khi lưu, dễ gây hỏng phân quyền.
[B]
`sudo rm -rf /etc/sudoers`
[EXP]
Sai. Lệnh này xóa file cấu hình sudoers sẽ làm hỏng hoàn toàn cơ chế sudo của hệ thống.
[C]
`cat /etc/sudoers`
[EXP]
Sai. Lệnh `cat` chỉ hiển thị nội dung file, không có tính năng chỉnh sửa.
[D]
`sudo visudo`
[EXP]
Đúng. Lệnh `visudo` mở file cấu hình và tự động kiểm tra lỗi cú pháp trước khi ghi đè lưu lại, ngăn ngừa lỗi cấu hình làm sập sudo.

@correct: D
@point: 20
@difficulty: 8
@concept: infrastructure-security
@category: 1

## Q25
Sau khi chỉnh sửa cấu hình cổng kết nối trong file `/etc/ssh/sshd_config`, các bạn cần chạy lệnh nào để áp dụng thay đổi mới?

[A]
`sudo systemctl restart ssh`
[EXP]
Đúng. Khởi động lại dịch vụ SSH daemon bằng lệnh này sẽ giúp hệ thống nạp cấu hình cổng mới.
[B]
`sudo apt update`
[EXP]
Sai. Lệnh này dùng để cập nhật danh sách gói phần mềm từ internet, không liên quan đến SSH.
[C]
`sudo ufw enable`
[EXP]
Sai. Lệnh này dùng để kích hoạt tường lửa UFW hoạt động, không khởi động lại SSH.
[D]
`ssh root@localhost`
[EXP]
Sai. Đây là lệnh tự kết nối SSH cục bộ, không dùng để nạp lại cấu hình dịch vụ.

@correct: A
@point: 20
@difficulty: 8
@concept: cloud-server-provisioning
@category: 1

## Q26
Trong tường lửa UFW của Ubuntu, lệnh nào dùng để xóa bỏ một luật cho phép kết nối cổng đã thiết lập trước đó?

[A]
`sudo ufw status verbose`
[EXP]
Sai. Lệnh này dùng để xem thông tin chi tiết trạng thái tường lửa, không dùng để xóa luật.
[B]
`sudo ufw delete allow <port>`
[EXP]
Đúng. Từ khóa `delete` đặt trước luật cho phép sẽ giúp gỡ bỏ luật đó khỏi cấu hình tường lửa.
[C]
`sudo ufw disable`
[EXP]
Sai. Lệnh này tắt toàn bộ tường lửa UFW, không phải xóa một luật cụ thể.
[D]
`sudo ufw default deny incoming`
[EXP]
Sai. Lệnh này thiết lập chính sách chặn mặc định cho lưu lượng đi vào, không dùng để xóa luật cụ thể.

@correct: B
@point: 20
@difficulty: 8
@concept: infrastructure-security
@category: 1

## Q27
Thư mục nào sau đây trong cấu hình Nginx chứa các file cấu hình website đã được kích hoạt chạy thực tế?

[A]
`/etc/nginx/sites-available/`
[EXP]
Sai. Thư mục này chứa các file cấu hình sẵn có nhưng chưa chắc đã được kích hoạt chạy thực tế.
[B]
`/var/log/nginx/`
[EXP]
Sai. Đây là thư mục chứa các tệp tin nhật ký log hoạt động, không chứa cấu hình chạy.
[C]
`/etc/nginx/sites-enabled/`
[EXP]
Đúng. Chỉ các cấu hình (hoặc symlink trỏ từ sites-available) nằm trong thư mục này mới được Nginx nạp chạy thực tế.
[D]
`/var/www/html/`
[EXP]
Sai. Đây là thư mục chứa mã nguồn tĩnh (HTML/CSS) của website, không chứa file cấu hình Nginx.

@correct: C
@point: 20
@difficulty: 8
@concept: nginx-basic-setup
@category: 1

## Q28
Mục đích của việc sử dụng chỉ thị `internal;` bên trong block `location = /custom_404.html` khi cấu hình Nginx là gì?

[A]
Cho phép mọi người dùng ngoài internet tải trực tiếp file custom_404.html về máy.
[EXP]
Sai. `internal` ngăn chặn người dùng ngoài internet truy cập trực tiếp file lỗi qua URL.
[B]
Tăng tốc độ đọc file từ đĩa cứng của máy chủ lên gấp hai lần.
[EXP]
Sai. Chỉ thị này kiểm soát phân quyền truy cập, không tối ưu tốc độ đọc đĩa cứng.
[C]
Bắt buộc Nginx phải ghi nhận toàn bộ log lỗi 404 vào file hệ thống chung.
[EXP]
Sai. Nhật ký log lỗi được điều khiển bởi chỉ thị `error_log`, không phải `internal`.
[D]
Chỉ cho phép Nginx chuyển hướng nội bộ sang file lỗi này, chặn người dùng gọi trực tiếp URL.
[EXP]
Đúng. Chỉ thị `internal;` bảo vệ các tài nguyên báo lỗi hoặc xử lý nội bộ không bị phơi bày trực tiếp ra ngoài.

@correct: D
@point: 20
@difficulty: 9
@concept: nginx-basic-setup
@category: 1

## Q29
Khi cấu hình xác thực Basic Authentication trong Nginx, tại sao các bạn không nên đặt tệp tin `.htpasswd` bên trong thư mục gốc `/var/www/html/` của website?

[A]
Vì người dùng ngoài internet có thể tải trực tiếp file mật khẩu này về để giải mã bẻ khóa.
[EXP]
Đúng. Đặt trong thư mục gốc sẽ khiến file bị phơi bày ra internet qua URL, kẻ xấu có thể tải về và thực hiện giải mã băm mật khẩu.
[B]
Vì Nginx sẽ bị lỗi cú pháp cấu hình và không thể khởi động lại dịch vụ.
[EXP]
Sai. Nginx vẫn khởi động được bình thường nhưng hệ thống sẽ bị mất an toàn bảo mật nghiêm trọng.
[C]
Vì hệ điều hành Ubuntu sẽ tự động xóa các file ẩn bắt đầu bằng dấu chấm.
[EXP]
Sai. Ubuntu không tự động xóa các file ẩn bắt đầu bằng dấu chấm.
[D]
Vì công cụ htpasswd chỉ hỗ trợ tạo file trong thư mục cấu hình mặc định /etc/nginx/.
[EXP]
Sai. htpasswd có thể tạo file ở bất kỳ thư mục nào tùy chỉ định của người dùng.

@correct: A
@point: 20
@difficulty: 9
@concept: nginx-basic-setup
@category: 1

## Q30
Sự khác biệt về cơ chế hoạt động khi các bạn chạy lệnh `systemctl restart nginx` và `systemctl reload nginx` là gì?

[A]
Lệnh restart chỉ chạy trên Windows còn lệnh reload chỉ chạy được trên Ubuntu.
[EXP]
Sai. Cả hai lệnh đều chạy trên các hệ thống Linux quản lý dịch vụ bằng systemd.
[B]
Lệnh restart ngắt dịch vụ và kết nối hiện tại để nạp lại, còn reload áp dụng cấu hình mới không gây gián đoạn.
[EXP]
Đúng. `restart` sẽ tắt hoàn toàn tiến trình Nginx rồi bật lại, còn `reload` chỉ gửi tín hiệu nạp lại cấu hình mới cho các worker process mà không ngắt kết nối đang hoạt động.
[C]
Lệnh reload sẽ tự động xóa sạch toàn bộ mã nguồn website tĩnh đang lưu trên ổ đĩa.
[EXP]
Sai. Không có lệnh quản lý dịch vụ nào tự ý xóa dữ liệu mã nguồn của website.
[D]
Lệnh restart giúp tăng gấp đôi dung lượng bộ nhớ RAM ảo của máy chủ ảo VPS.
[EXP]
Sai. Khởi động lại dịch vụ không làm thay đổi tài nguyên phần cứng vật lý hay ảo hóa cấp phát cho VPS.

@correct: B
@point: 20
@difficulty: 9
@concept: nginx-basic-setup
@category: 1
