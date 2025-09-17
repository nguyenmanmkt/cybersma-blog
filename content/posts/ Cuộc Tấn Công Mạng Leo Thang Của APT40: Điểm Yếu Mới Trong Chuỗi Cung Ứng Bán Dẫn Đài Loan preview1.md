---
title: "Cuộc Tấn Công Mạng Leo Thang Của APT40: Điểm Yếu Mới Trong Chuỗi Cung Ứng Bán Dẫn Đài Loan"
date: 2025-09-17T15:53:22.516+07:00
draft: false
tags: ["APT40", "semiconductor", "chuỗi cung ứng", "Đài Loan", "Visual Studio Code Remote Tunnel", "Google Sheets C2", "gián điệp mạng", "TTPs", "Voldemort", "HealthKick"]
categories: ["Cyber Security", "Software Tool"]
---

## Mở đầu

Trong bối cảnh căng thẳng thương mại Mỹ-Trung Quốc ngày càng gia tăng, an ninh mạng đang trở thành một mặt trận chiến lược quan trọng. Ngành công nghiệp bán dẫn, xương sống của nền kinh tế kỹ thuật số toàn cầu, đặc biệt là chuỗi cung ứng tại Đài Loan, đang đối mặt với những mối đe dọa ngày càng tinh vi. Gần đây, nhóm gián điệp mạng **APT40** (còn được biết đến là TA415), một tổ chức có liên kết chặt chẽ với Trung Quốc, đã tăng cường đáng kể các chiến dịch tấn công mạng nhắm vào các nhà sản xuất bán dẫn, các thực thể trong chuỗi cung ứng và cả các nhà phân tích đầu tư tại khu vực này [N1, N2].

![TA415 tấn công chuỗi cung ứng bán dẫn Đài Loan](/images/2025/China-aligned-TA415-escalates-cyberattacks-on-taiwanese-semiconductor-manufacturing-supply-chains.webp)

Các cuộc tấn công này không chỉ thể hiện sự leo thang về tần suất mà còn cho thấy sự phát triển trong **kỹ thuật, chiến thuật và quy trình (TTPs)** của các nhóm liên kết Trung Quốc. Nhóm APT41, một nhóm gián điệp mạng khác của Trung Quốc, đã lợi dụng các công cụ đám mây hợp pháp và các tính năng như **Visual Studio Code Remote Tunnel** để thiết lập quyền truy cập từ xa bền bỉ. Trong khi đó, các chiến dịch khác sử dụng **Google Sheets làm cơ sở hạ tầng Command-and-Control (C2)**, khiến việc phát hiện trở nên phức tạp hơn [N1, N3].

Bài viết này sẽ đi sâu phân tích các TTPs mới của các nhóm gián điệp mạng liên quan Trung Quốc, bối cảnh các cuộc tấn công, và đưa ra các khuyến nghị thiết thực để các tổ chức bảo vệ mình khỏi những mối đe dọa gián điệp mạng ngày càng phức tạp này.

## APT40: Nhóm Gián điệp Mạng Trung Quốc

APT40, còn được biết đến với các tên gọi khác như **TA415, Kryptonite Panda, Gingham Typhoon, Leviathan, hoặc Bronze Mohawk**, là một nhóm gián điệp mạng được cho là do nhà nước Trung Quốc tài trợ, liên kết chặt chẽ với Bộ An ninh Quốc gia (MSS) của Trung Quốc. Mục tiêu chính của nhóm là thu thập thông tin tình báo kinh tế và công nghệ có giá trị cao từ các mục tiêu chiến lược [N6].

Ban đầu, APT40 tập trung vào các lĩnh vực như hàng không vũ trụ và hóa chất. Tuy nhiên, trong các chiến dịch gần đây, phạm vi tấn công của chúng đã mở rộng đáng kể, bao gồm:

*   Các tổ chức chính phủ Hoa Kỳ.
*   Các tổ chức học thuật và viện nghiên cứu [N1, N6].
*   Và đặc biệt là ngành sản xuất bán dẫn và chuỗi cung ứng liên quan tại Đài Loan [N1, N2].

Sự mở rộng này phản ánh trọng tâm chiến lược của Trung Quốc trong việc thu thập thông tin tình báo về chuỗi cung ứng bán dẫn, một lĩnh vực cực kỳ nhạy cảm và cạnh tranh toàn cầu.

## Sự Leo Thang Tấn Công Vào Ngành Bán Dẫn Đài Loan

Từ tháng 3 đến tháng 6 năm 2025, các nhóm gián điệp mạng liên kết Trung Quốc, bao gồm cả APT40, đã tập trung cao độ vào các nhà sản xuất, nhà thiết kế bán dẫn, các công ty trong chuỗi cung ứng và các nhà phân tích thị trường liên quan đến Đài Loan [N1, N2]. Các chiến dịch spear-phishing (lừa đảo có chủ đích) đã được phát hiện vào tháng 7 và tháng 8, nhắm vào các tổ chức chính phủ Mỹ và các tổ chức hoạch định chính sách kinh tế với những chiêu bài liên quan đến kinh tế Mỹ-Trung.

Các chủ đề lừa đảo thường được sử dụng bao gồm:
*   Mời ứng tuyển việc làm giả mạo.
*   Đề nghị hợp tác kinh doanh không có thật [N1, N2].

Điều này cho thấy các nhóm APT của Trung Quốc có khả năng tùy chỉnh các chiến dịch của mình để phù hợp với mục tiêu cụ thể, tăng hiệu quả của các cuộc tấn công ban đầu.

## TTPs Đổi Mới Của Các Nhóm APT Liên Kết Trung Quốc

Các nhóm gián điệp mạng liên kết Trung Quốc đã liên tục đổi mới TTPs của mình để né tránh các giải pháp bảo mật truyền thống, tập trung vào việc lợi dụng các công cụ hợp pháp và dịch vụ đám mây.

### Spear-Phishing Tinh Vi

Các chiến dịch spear-phishing của các nhóm này rất được đầu tư, với nội dung được cá nhân hóa cao. Chúng thường sử dụng các chủ đề liên quan đến ngành nghề của nạn nhân hoặc các sự kiện thời sự (như căng thẳng thương mại Mỹ-Trung) để tăng tỷ lệ thành công.

### Khai Thác Visual Studio Code Remote Tunnel

Một trong những TTPs đáng chú ý nhất gần đây là việc nhóm **APT41 (Stately Taurus)** khai thác **Visual Studio Code (VS Code) Remote Tunnel** [N4, N7]. Kể từ tháng 9 năm 2024, nhóm này đã chuyển hướng sang việc cung cấp quyền truy cập qua VS Code Remote Tunnel thay vì chỉ đơn thuần triển khai malware truyền thống.

*   **Cách thức khai thác:** Kẻ tấn công sử dụng một bộ tải Python được làm xáo trộn, gọi là **WhirlCoil**, để thiết lập đường hầm từ xa của VS Code [N4, N7]. WhirlCoil sử dụng các tệp .LNK độc hại để tải xuống và thực thi một tập lệnh Python, sau đó khởi tạo một Remote Tunnel và lấy mã kích hoạt để xác thực qua tài khoản GitHub, cho phép kiểm soát máy nạn nhân từ xa [N4].
*   **Ưu điểm cho kẻ tấn công:**
    *   **Truy cập bền bỉ và bí mật:** Tính năng Remote Tunnel được thiết kế để nhà phát triển làm việc từ xa, do đó, lưu lượng truy cập qua đường hầm này trông hoàn toàn hợp pháp. Điều này giúp kẻ tấn công hòa lẫn vào lưu lượng mạng thông thường, rất khó bị phát hiện bởi các công cụ giám sát mạng truyền thống [N4].
    *   **Vượt qua các giải pháp bảo mật:** Vì đây là một tính năng hợp pháp, nhiều giải pháp bảo mật không được cấu hình để cảnh báo về hoạt động này.

### Sử Dụng Google Sheets & Calendar làm C2

Các nhóm APT liên kết Trung Quốc, đặc biệt là **APT41**, thường lạm dụng các dịch vụ đám mây hợp pháp như **Google Sheets và Google Calendar** để làm cơ sở hạ tầng **Command-and-Control (C2)** [N3, N8].

*   **Cách thức:** Kẻ tấn công nhúng các lệnh hoặc thông tin C2 vào các bảng tính Google Sheets hoặc các sự kiện Google Calendar. Malware trên máy nạn nhân sẽ truy vấn các tài liệu này để nhận lệnh hoặc gửi dữ liệu.
*   **Ưu điểm cho kẻ tấn công:**
    *   **Ngụy trang hoạt động độc hại:** Việc sử dụng các dịch vụ của Google giúp các hoạt động C2 hòa lẫn vào lưu lượng truy cập đám mây hợp pháp, khối lượng lớn, khiến các hệ thống phát hiện khó phân biệt hoạt động độc hại với hoạt động hợp pháp của người dùng.
    *   **Phân phối Malware:** Trong các hoạt động đầu năm 2024, một backdoor tùy chỉnh có tên **Voldemort** đã được triển khai, có khả năng sử dụng Google Sheets cho C2 và thậm chí lưu trữ các tệp tìm kiếm trên các chia sẻ mạng bên ngoài [N3, N9]. Ngoài ra, nhóm APT41 đã sử dụng malware **TOUGHPROGRESS** để khai thác Google Calendar cho C2 thông qua kỹ thuật DLL sideloading [N8].

### Bảng Tóm Tắt TTPs Gần Đây Của Các Nhóm APT Liên Kết Trung Quốc

| Kỹ thuật hoặc Công cụ       | Mục đích / Lạm dụng                                | Bối cảnh / Chi tiết                                                                | Liên kết APT chính |
| :-------------------------- | :------------------------------------------------- | :--------------------------------------------------------------------------------- | :----------------: |
| VS Code Remote Tunnel       | Truy cập bền bỉ, né tránh phát hiện               | Được sử dụng trong các chuỗi phishing từ tháng 9/2024, phân phối qua WhirlCoil [N4] | APT41 (Stately Taurus) |
| Google Sheets               | Command & Control tàng hình                        | Được sử dụng trong Voldemort và các kênh C2 malware khác [N3, N9]                  | APT41 và các nhóm khác |
| Google Calendar             | C2 thay thế và giao tiếp beacon                   | Giúp hòa lẫn vào lưu lượng truy cập thông thường [N8]                              | APT41 (TOUGHPROGRESS) |
| DLL Sideloading             | Né tránh phát hiện malware                        | Triển khai backdoor TOUGHPROGRESS [N8]                                             | APT41 |
| Cobalt Strike, Voldemort    | Implant, di chuyển ngang, tải trọng bổ sung       | Các chiến dịch lặp lại năm 2024, bao gồm mục tiêu bán dẫn [N1, N2]                  | Các nhóm liên kết Trung Quốc |
| Obfuscated Python Loaders   | Phân phối tải trọng ban đầu                       | Ví dụ: WhirlCoil để thiết lập đường hầm từ xa [N4]                                 | APT41 |

## Ảnh Hưởng và Rủi Ro

Ngành công nghiệp bán dẫn là huyết mạch của mọi công nghệ hiện đại, từ điện thoại thông minh đến trung tâm dữ liệu. Một cuộc tấn công thành công vào chuỗi cung ứng bán dẫn có thể gây ra những hậu quả nghiêm trọng:
*   **Gián đoạn sản xuất:** Ảnh hưởng đến khả năng sản xuất chip toàn cầu.
*   **Mất cắp sở hữu trí tuệ:** Đe dọa khả năng cạnh tranh và đổi mới.
*   **Tác động kinh tế:** Gây thiệt hại tài chính lớn và làm suy yếu niềm tin vào thị trường.

Sự phức tạp của môi trường công nghệ hiện đại, đặc biệt là việc áp dụng nhanh chóng kiến trúc hybrid và multi-cloud, cùng với sự tích hợp AI đang tạo ra những "điểm mù" và sự phức tạp mới trong bảo mật [N5, N10]. Các tổ chức thường vận hành nhiều môi trường riêng biệt, dẫn đến quản lý danh tính phân mảnh và giám sát rủi ro không nhất quán. Tầm nhìn rời rạc và quyền hạn quá mức đang khiến các doanh nghiệp dễ bị tấn công đám mây, thường trầm trọng hơn do sự lan rộng của khối lượng công việc được điều khiển bởi AI [N5, N10]. Dù nhiều tổ chức đang triển khai giám sát hợp nhất và quản lý tư thế bảo mật đám mây (CSPM), tầm nhìn rộng và hiệu quả vẫn còn hạn chế [N5, N10].

## Khuyến Nghị Phòng Thủ

Để chống lại các TTPs ngày càng tinh vi của APT40 và các nhóm gián điệp mạng khác của Trung Quốc, các tổ chức cần áp dụng một chiến lược bảo mật đa lớp và chủ động:

*   **Giám sát hoạt động VS Code Tunnel bất thường:**
    *   Thực hiện giám sát chặt chẽ lưu lượng mạng liên quan đến VS Code Remote Tunnel.
    *   Tìm kiếm các kết nối từ xa dựa trên GitHub đáng ngờ, đặc biệt là từ các máy trạm không thuộc nhóm phát triển hoặc có hành vi sử dụng bất thường.
    *   Tích hợp nhật ký VS Code vào hệ thống SIEM/SOC để phân tích.
*   **Kiểm tra lưu lượng truy cập Google Sheets/Calendar đáng ngờ:**
    *   Giám sát lưu lượng mạng đến và đi từ các dịch vụ của Google, đặc biệt là Google Sheets và Google Calendar.
    *   Tìm kiếm các tác nhân người dùng (user agents) không điển hình hoặc quyền truy cập bất ngờ vào các tài liệu bên ngoài.
    *   Sử dụng các giải pháp Cloud Access Security Broker (CASB) để giám sát và kiểm soát việc sử dụng các ứng dụng đám mây.
*   **Nâng cao nhận thức về phishing:**
    *   Thường xuyên đào tạo và nâng cao nhận thức cho nhân viên về các chiến dịch phishing, đặc biệt là những email có chủ đề liên quan đến ngành, các cơ hội việc làm hoặc lời mời hợp tác hấp dẫn.
    *   Triển khai các cuộc diễn tập phishing để đánh giá mức độ phản ứng của nhân viên.
*   **Triển khai bảo mật đa lớp:**
    *   Sử dụng xác thực đa yếu tố (MFA) cho tất cả các dịch vụ, đặc biệt là các tài khoản quản trị và truy cập từ xa.
    *   Thực hiện phân đoạn mạng để hạn chế sự di chuyển ngang của kẻ tấn công.
    *   Cập nhật và vá lỗi hệ thống thường xuyên.
    *   Sử dụng các giải pháp Endpoint Detection and Response (EDR) và Extended Detection and Response (XDR) để phát hiện và phản ứng sớm.
*   **Quản lý tư thế bảo mật đám mây (CSPM):**
    *   Đảm bảo cấu hình bảo mật đúng đắn cho các môi trường đám mây (hybrid, multi-cloud).
    *   Thường xuyên kiểm tra các quyền truy cập quá mức và các điểm mù bảo mật trong các hệ thống đám mây.

## Kết Luận

Cuộc tấn công leo thang của APT40 và các nhóm gián điệp mạng liên kết Trung Quốc vào chuỗi cung ứng bán dẫn Đài Loan là một lời nhắc nhở rõ ràng về sự phức tạp và tinh vi của gián điệp mạng hiện đại. Bằng cách khai thác các công cụ và dịch vụ đám mây hợp pháp, các nhóm này đã tạo ra một mô hình tấn công khó bị phát hiện và gây ra mối đe dọa đáng kể. Các tổ chức trong ngành công nghiệp bán dẫn và các lĩnh vực quan trọng khác cần phải chủ động cập nhật các chiến lược phòng thủ của mình, tập trung vào giám sát hành vi, nhận diện các TTPs mới và nâng cao nhận thức cho toàn bộ nhân viên để bảo vệ tài sản thông tin quý giá của mình.

## Nguồn Tham Khảo

*   [N1] China-aligned TA415 escalates cyberattacks on Taiwanese semiconductor manufacturing, supply chains. Industrial Cyber. 2025-09-17.
*   [N2] Chinese state-aligned hackers target TSMC and Taiwan semiconductor supply chain. WebProNews. 2025-07-17.
*   [N3] New Voldemort Malware Espionage Campaign. Proofpoint. 2024-08-29.
*   [N4] VSCode Remote Tunnels exploited in suspected Chinese cyberespionage campaign. SC Media. 2024-12-11.
*   [N5] Organisations are struggling to keep pace with Cloud Security challenges. Tahawultech. 2025-09-17.
*   [N6] Cybersecurity Agencies Warn of China-based Cyber Group. The Hacker News. 2024-07-09.
*   [N7] Chinese Hackers Exploit Visual Studio Code in Southeast Asian Governments. The Hacker News. 2024-09-09.
*   [N8] Chinese APT41 Exploits Google Calendar in Cyberattacks. The Record. 2025-05-13.
*   [N9] New Voldemort Malware Abuses Google Sheets To Store Stolen Data. BleepingComputer. 2024-08-29.
*   [N10] 2025 State of Cloud Security Report. Orca Security. 2025-09-17.