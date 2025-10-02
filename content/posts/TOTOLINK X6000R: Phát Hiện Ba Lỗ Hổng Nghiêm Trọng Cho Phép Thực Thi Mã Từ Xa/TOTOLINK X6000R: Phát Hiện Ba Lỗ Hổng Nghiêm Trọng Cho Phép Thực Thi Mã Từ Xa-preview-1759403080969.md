---
title: "TOTOLINK X6000R: Phát Hiện Ba Lỗ Hổng Nghiêm Trọng Cho Phép Thực Thi Mã Từ Xa"
date: 2025-10-02T18:03:24.158+07:00
draft: false
tags: ["An ninh mạng", "Bảo mật hệ thống", "Lỗ hổng bảo mật", "Tấn công mạng", "Phòng thủ mạng", "Quản lý rủi ro", "Firewall", "Endpoint Security", "TOTOLINK", "X6000R", "RCE", "Command Injection", "Argument Injection", "Security Bypass"]
categories: ["Cyber Security"]
---

![Tấn công TOTOLINK X6000R](static/images/2025/TOTOLINK X6000R Routers Hit by Three Vulnerabilities Allowing Remote Code Execution/docker%20termux%20flaw%20%281%29%20%281%29%20%281%29.webp)

## Mở đầu: Nguy Cơ Từ Router Bị Lỗ Hổng Bảo Mật

Router là trái tim của mọi mạng gia đình và doanh nghiệp nhỏ, đóng vai trò cầu nối quan trọng giữa các thiết bị nội bộ và internet. Tuy nhiên, nếu không được bảo vệ đúng cách, router có thể trở thành điểm yếu nghiêm trọng, mở ra cánh cửa cho các cuộc tấn công mạng. Gần đây, ba lỗ hổng bảo mật nghiêm trọng đã được phát hiện trong các bộ định tuyến TOTOLINK X6000R, phiên bản firmware V9.4.0cu.1360_B20241207 (phát hành ngày 28 tháng 3 năm 2025). Những lỗ hổng này có thể cho phép kẻ tấn công thực thi mã từ xa (Remote Code Execution - RCE), gây ra hậu quả nghiêm trọng cho người dùng và hệ thống mạng của họ [N1, N2].

## Chi tiết về các Lỗ hổng trong TOTOLINK X6000R

Các lỗ hổng được phát hiện bao gồm lỗi tiêm đối số (argument injection), tiêm lệnh (command injection) và bỏ qua cơ chế bảo mật (security bypass), tất cả đều có thể bị khai thác từ xa [1].

### Lỗ hổng 1: CVE-2025-52905 – Argument Injection

*   **Đánh giá:** Cao (High)
*   **Điểm CVSS-B:** 7.0
*   **Mô tả:** Lỗ hổng tiêm đối số này xảy ra do việc lọc không đầy đủ các ký tự đặc biệt, có thể khiến router bị treo hoặc làm quá tải các máy chủ bên ngoài, dẫn đến một cuộc tấn công từ chối dịch vụ (Denial-of-Service - DoS) [N1, N3, 1]. Khi bị khai thác, router sẽ không thể hoạt động bình thường, làm gián đoạn toàn bộ kết nối internet của người dùng. Lỗ hổng này ảnh hưởng đến các phiên bản firmware của TOTOLINK X6000R tới và bao gồm V9.4.0cu.1360_B20241207 [4, 10].

### Lỗ hổng 2: CVE-2025-52906 – Unauthenticated Command Injection

*   **Đánh giá:** Nghiêm trọng (Critical)
*   **Điểm CVSS-B:** 9.3
*   **Mô tả:** Đây là lỗ hổng tiêm lệnh không yêu cầu xác thực, cho phép kẻ tấn công thực thi các lệnh tùy ý trên thiết bị từ xa. Cụ thể, lỗ hổng này nằm trong hàm `setEasyMeshAgentCfg` và cho phép thực thi lệnh với quyền root mà không cần thông tin đăng nhập [1, 2, 3, 5, 7, 9]. Với mức điểm CVSS-B cực cao (9.3), lỗ hổng này đặc biệt nguy hiểm vì nó không yêu cầu bất kỳ thông tin đăng nhập nào để khai thác, mang lại cho kẻ tấn công quyền kiểm soát đáng kể đối với router [N1, N3].
![Lỗ hổng Command Injection](static/images/2025/TOTOLINK X6000R Routers Hit by Three Vulnerabilities Allowing Remote Code Execution/word-image-260112-159831-1.png)

### Lỗ hổng 3: CVE-2025-52907 – Security Bypass

*   **Đánh giá:** Cao (High)
*   **Điểm CVSS-B:** 7.3
*   **Mô tả:** Lỗ hổng bỏ qua bảo mật này có thể bị khai thác để thực hiện ghi file tùy ý, gây ra DoS liên tục, hoặc kết hợp với các lỗ hổng khác để đạt được quyền thực thi mã từ xa. Lỗ hổng này bỏ qua cơ chế kiểm tra đầu vào, cho phép kẻ tấn công thay đổi cấu hình hệ thống hoặc cài đặt phần mềm độc hại, dẫn đến thỏa hiệp hệ thống nghiêm trọng [N1, N3, 1]. Khả năng ghi file tùy ý cho phép kẻ tấn công thay đổi cấu hình hệ thống hoặc cài đặt phần mềm độc hại, dẫn đến thỏa hiệp hệ thống nghiêm trọng [1, 6, 8].
![Kiến trúc lỗ hổng](static/images/2025/TOTOLINK X6000R Routers Hit by Three Vulnerabilities Allowing Remote Code Execution/word-image-262762-159831-2.png)

## Cách thức Khai thác và Tác động

Sự kết hợp của ba lỗ hổng này tạo ra một kịch bản tấn công đáng lo ngại. Kẻ tấn công có thể:

*   **Thực thi mã từ xa (RCE):** Đây là mục tiêu cuối cùng của nhiều cuộc tấn công, cho phép kẻ tấn công chạy bất kỳ lệnh nào trên router, biến thiết bị thành một phần của mạng botnet, thực hiện các cuộc tấn công khác hoặc thu thập thông tin nhạy cảm.
*   **Tấn công từ chối dịch vụ (DoS):** Làm gián đoạn hoàn toàn kết nối internet, gây thiệt hại đáng kể cho các doanh nghiệp và người dùng phụ thuộc vào mạng.
*   **Ghi file tùy ý:** Thay đổi cài đặt hệ thống, tiêm mã độc vào firmware, hoặc xóa các file quan trọng, gây hư hỏng thiết bị hoặc mất dữ liệu.
*   **Truy cập trái phép:** Các lỗ hổng này có thể được sử dụng để chiếm quyền truy cập vào mạng nội bộ, mở đường cho các cuộc tấn công sâu hơn vào các thiết bị khác trong mạng.

Một lỗ hổng khác, **CVE-2024-7907**, cũng đã được ghi nhận ảnh hưởng đến phiên bản firmware cũ hơn (9.4.0cu.852_20230719), liên quan đến tiêm lệnh trong hàm `setSyslogCfg` thông qua đối số `rtLogServer` [N4]. Mặc dù không nằm trong ba lỗ hổng mới nhất, điều này cho thấy lịch sử lỗ hổng bảo mật của dòng sản phẩm này.

## Biện pháp Khắc phục và Khuyến nghị

Để bảo vệ router TOTOLINK X6000R của bạn khỏi các mối đe dọa này, điều quan trọng nhất là phải thực hiện các bước sau:

1.  **Cập nhật Firmware Ngay lập tức:**
    *   TOTOLINK đã phát hành bản vá lỗi. Người dùng nên cập nhật firmware lên phiên bản mới nhất: **V9.4.0cu.1498_B20250826** [N1, N2, 1].
    *   Kiểm tra trang web chính thức của TOTOLINK hoặc giao diện quản lý router của bạn để tải xuống và cài đặt bản cập nhật.

2.  **Thay đổi Mật khẩu Mặc định:**
    *   Luôn thay đổi mật khẩu mặc định của router thành mật khẩu mạnh, phức tạp.
    *   Sử dụng kết hợp chữ hoa, chữ thường, số và ký tự đặc biệt.

3.  **Tắt Các Dịch vụ Không Cần Thiết:**
    *   Kiểm tra và tắt các dịch vụ không cần thiết như Telnet, SSH (nếu không sử dụng), hoặc quản lý từ xa qua WAN (nếu không thực sự cần).
    *   Giới hạn quyền truy cập vào giao diện quản lý router chỉ từ mạng nội bộ.

4.  **Sử dụng Tường lửa:**
    *   Đảm bảo tường lửa của router được cấu hình đúng cách để chặn các truy cập không mong muốn từ bên ngoài.
    *   Cân nhắc sử dụng tường lửa thế hệ tiếp theo (Next-Generation Firewall - NGFW) với tính năng ngăn chặn mối đe dọa (Threat Prevention) hoặc ngăn chặn mối đe dọa nâng cao (Advanced Threat Prevention) nếu có thể, như Palo Alto Networks khuyến nghị để chặn các cuộc tấn công [N3].

5.  **Theo dõi Các Thông báo Bảo mật:**
    *   Thường xuyên theo dõi các nguồn tin tức về bảo mật để nắm bắt thông tin về các lỗ hổng mới và bản vá lỗi.

## Kết luận

Các lỗ hổng nghiêm trọng trong router TOTOLINK X6000R là một lời nhắc nhở quan trọng về sự cần thiết của việc duy trì bảo mật mạng. Việc cập nhật firmware là bước then chốt để bảo vệ thiết bị của bạn khỏi các cuộc tấn công thực thi mã từ xa. Đừng bỏ qua các cảnh báo bảo mật, bởi một router bị tổn hại có thể mở ra những rủi ro lớn cho toàn bộ hệ thống mạng của bạn.

## Nguồn Tham Khảo

*   **N1:** [gbhackers.com - TOTOLINK X6000R Routers Hit by Three Vulnerabilities Allowing Remote Code Execution](https://gbhackers.com/totolink-x6000r-routers-hit-by-three-vulnerabilities/)
*   **N2:** [cyberpress.org - Three New Vulnerabilities in TOTOLINK X6000R Routers Allow Remote Code Execution](https://cyberpress.org/totolink-x6000r-routers/)
*   **N3:** [unit42.paloaltonetworks.com - TOTOLINK X6000R: Three New Vulnerabilities Uncovered](https://unit42.paloaltonetworks.com/totolink-x6000r-vulnerabilities/)
*   **N4:** [cvedetails.com - CVE-2024-7907](https://www.cvedetails.com/cve/CVE-2024-7907/)
*   [1] Critical Flaw CVE-2025-52906 (CVSS 9.3) Allows Unauthenticated ... (2025, October 2). SecurityOnline.info. Truy cập từ: https://securityonline.info/critical-flaw-cve-2025-52906-cvss-9-3-allows-unauthenticated-rce-on-totolink-x6000r-routers/
*   [2] CVE-2025-52906 - Exploits & Severity - Feedly. (2025, September 25). Feedly. Truy cập từ: https://feedly.com/cve/CVE-2025-52906
*   [3] CVE Record: CVE-2025-52906 - Mitre. (2025, September 24). Mitre.org. Truy cập từ: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2025-52906
*   [4] CVE-2025-52905 | Tenable®. (2025, October 2). Tenable.com. Truy cập từ: https://www.tenable.com/cve/CVE-2025-52905
*   [5] CVE-2025-52906 - NVD. (2025, September 25). Nvd.nist.gov. Truy cập từ: https://nvd.nist.gov/vuln/detail/CVE-2025-52906
*   [6] CVE-2025-52907 | Tenable®. (2025, September 27). Tenable.com. Truy cập từ: https://www.tenable.com/cve/CVE-2025-52907
*   [7] Totolink CVEs and Security Vulnerabilities - OpenCVE. (2025, October 1). Opencve.io. Truy cập từ: https://app.opencve.io/cve/?vendor=totolink
*   [8] CVE-2025-52907 : Improper Input Validation vulnerability in ... (2025, September 24). Cvedetails.com. Truy cập từ: https://www.cvedetails.com/cve/CVE-2025-52907/
*   [9] CVE-2025-52906 | Tenable®. (2025, October 2). Tenable.com. Truy cập từ: https://www.tenable.com/cve/CVE-2025-52906
*   [10] CVE-2025-52905 - CVE Record. (2025, September 23). Cve.org. Truy cập từ: https://www.cve.org/CVERecord?id=CVE-2025-52905