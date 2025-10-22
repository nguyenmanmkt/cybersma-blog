---
title: "F5 Bị Tấn Công Bởi Quốc Gia: Mã Nguồn BIG-IP Lộ, Nguy Cơ Zero-Day Tăng Cao"
date: 2025-10-22T07:02:51.995+07:00
draft: false
tags: ["An ninh mạng", "Bảo mật hệ thống", "Lỗ hổng bảo mật", "Tấn công mạng", "Phòng thủ mạng", "Quản lý rủi ro", "Giám sát bảo mật", "Threat Intelligence", "Endpoint Security", "Firewall"]
categories: ["Cyber Security"]
---

![F5 Bị Tấn Công Bởi Quốc Gia: Mã Nguồn BIG-IP Lộ, Nguy Cơ Zero-Day Tăng Cao](static/images/2025/F5 Bị Tấn Công Bởi Quốc Gia: Mã Nguồn BIG-IP Lộ, Nguy Cơ Zero-Day Tăng Cao/WvBYgg3DiH9a4NENQJueTg.jpg)

### Bối Cảnh Vụ Tấn Công

F5 đã phát hiện vào tháng 8 năm 2025 rằng một tác nhân đe dọa có trình độ cao, được cho là thuộc nhà nước, đã duy trì quyền truy cập dai dẳng và tải xuống các tệp từ môi trường phát triển sản phẩm và kỹ thuật của F5 trong nhiều tháng [1, 2, 3]. Mặc dù F5 đã thực hiện các biện pháp khẩn cấp để ngăn chặn và điều tra, nhưng vụ việc đã ảnh hưởng nghiêm trọng đến niềm tin của khách hàng và đặt ra thách thức lớn về bảo mật.

### Vectơ Tấn Công và Dữ Liệu Bị Đánh Cắp

*   **Vectơ xâm nhập ban đầu:** F5 chưa công bố chi tiết về vectơ xâm nhập ban đầu. Tuy nhiên, tác nhân đe dọa đã đạt được quyền truy cập dai dẳng, kéo dài vào môi trường phát triển sản phẩm và kỹ thuật của F5 [2, 3].
*   **Mục tiêu và dữ liệu bị đánh cắp:**
    *   **Mã nguồn BIG-IP:** Các phần của mã nguồn BIG-IP đã bị đánh cắp, cho phép kẻ tấn công phân tích để tìm kiếm các lỗ hổng mới và chưa được công bố (zero-day) [1, 4].
    *   **Dữ liệu lỗ hổng nội bộ:** Thông tin chi tiết về các lỗ hổng đã được phát hiện nhưng chưa được vá cũng bị lấy đi, cung cấp "lộ trình" cho các cuộc tấn công trong tương lai [1, 4].
    *   **Tệp cấu hình khách hàng:** Một phần nhỏ tệp cấu hình của các khách hàng giá trị cao cũng bị đánh cắp, tạo điều kiện cho các cuộc tấn công có mục tiêu cao hơn, được tùy chỉnh theo thiết lập thiết bị thực tế của họ [4, 6].
*   **Phân tích ảnh hưởng:** Với quyền truy cập vào mã nguồn và tài liệu thiết kế/nội bộ, kẻ tấn công có thể xác định và vũ khí hóa hiệu quả các lỗ hổng ẩn trong các ngăn xếp phần mềm của F5, có khả năng kích hoạt các cuộc tấn công firmware hoặc logic phức tạp [1, 4].

F5 đã khẳng định rằng không có bằng chứng về việc truy cập vào các hệ thống hỗ trợ khách hàng, tài chính, CRM, iHealth hoặc NGINX [4].

### Các Lỗ Hổng CVE Liên Quan (Tính đến tháng 10 năm 2025)

Mặc dù các mã định danh cụ thể như CVE-2025-53868, CVE-2025-61955 và CVE-2025-57780 được liệt kê trong yêu cầu, các lỗ hổng này đã được xác nhận và công bố bởi F5 sau sự cố bảo mật. Chúng bao gồm:

*   **CVE-2025-53868:** Lỗ hổng bỏ qua xác thực SCP/SFTP trong BIG-IP (chế độ Appliance). Kẻ tấn công có đặc quyền cao có thể lợi dụng việc làm sạch lệnh không đúng cách để bỏ qua các hạn chế của chế độ Appliance, dẫn đến truy cập hệ thống trái phép [11, 12].
*   **CVE-2025-61955** và **CVE-2025-57780:** Cả hai đều là lỗ hổng leo thang đặc quyền trong hệ thống F5OS (F5OS-A và F5OS-C). Kẻ tấn công đã được xác thực với quyền truy cập cục bộ có thể leo thang đặc quyền qua các ranh giới bảo mật, làm tăng đáng kể rủi ro bằng cách cho phép xâm phạm tính toàn vẹn và bảo mật của hệ thống [11, 13, 14].

Việc khai thác thực tế các lỗ hổng *chưa được tiết lộ* vẫn chưa được xác nhận, nhưng việc đánh cắp mã nguồn và nghiên cứu nội bộ đe dọa sự phát triển nhanh chóng các khai thác zero-day mới của các tác nhân đe dọa [1, 4].

### Biện Pháp Giảm Thiểu và Khuyến Nghị

F5 cùng các cơ quan an ninh mạng lớn trên thế giới đã đưa ra các khuyến nghị khẩn cấp cho người dùng BIG-IP, F5OS và BIG-IQ:

1.  **Cập nhật ngay lập tức lên các bản vá mới nhất:**
    *   Áp dụng tất cả các bản cập nhật bảo mật F5 có sẵn được phát hành sau tháng 10 năm 2025, bao gồm các Thông báo Bảo mật Hàng quý [1, 10].
2.  **Xoay vòng thông tin xác thực và khóa ký:**
    *   Thay đổi tất cả thông tin xác thực và khóa ký trên tất cả các nền tảng F5, tương tự như những gì F5 đã thực hiện nội bộ [3, 5].
3.  **Xem xét và áp dụng hướng dẫn tăng cường bảo mật mới:**
    *   Áp dụng các hướng dẫn tăng cường bảo mật do F5 và các cơ quan an ninh cung cấp, bao gồm kiểm soát truy cập nâng cao và các ranh giới quản trị/logic chặt chẽ hơn cho các thiết bị F5 và giao diện quản lý [6, 10].
4.  **Giám sát các chỉ số xâm nhập (IoCs):**
    *   Sử dụng các công cụ và mẫu IoC do F5 phát hành, đồng thời tích hợp với các hệ thống phát hiện và phản hồi điểm cuối (EDR) [6, 10].
5.  **Kiểm toán cấu hình khách hàng:**
    *   Hạn chế quyền truy cập quản trị viên chỉ cho những người dùng thiết yếu [6].
6.  **Tuân thủ các chỉ thị khẩn cấp:**
    *   Tuân thủ các chỉ thị khẩn cấp (như CISA ED 26-01) và hướng dẫn của NCSC cho các môi trường nhạy cảm về an ninh quốc gia, do mối đe dọa gia tăng [6, 7].
7.  **Đánh giá cấu hình bị ảnh hưởng:**
    *   F5 khuyên các khách hàng bị ảnh hưởng (đã được thông báo) với dữ liệu cấu hình bị lộ nên tiến hành *đánh giá cụ thể* và tăng cường bảo mật theo hướng dẫn [5].

### Kết Luận

Rủi ro chính từ sự cố bảo mật F5 này là khả năng tác nhân đe dọa vũ khí hóa các lỗ hổng mới hoặc hiện có để tấn công người dùng sản phẩm F5, đặc biệt là những người có cấu hình bị lộ [1, 4]. Ngay cả những khách hàng không bị ảnh hưởng trực tiếp bởi các cấu hình bị rò rỉ cũng phải hành động: *nâng cấp, tăng cường bảo mật và giám sát chặt chẽ* là điều cần thiết để chống lại nguy cơ khai thác có mục tiêu và phổ biến ngày càng tăng [6, 10].

### Nguồn Tham Khảo

*   [1] Nation-State Threat Actor Steals F5 Source Code. (2025, October 15). Unit 42. Truy cập từ: https://unit42.paloaltonetworks.com/nation-state-threat-actor-steals-f5-source-code/
*   [2] F5 admits nation-state actor stole BIG-IP source code. (2025, October 15). Computer Weekly. Truy cập từ: https://www.computerweekly.com/news/366632799/F5-admits-nation-state-actor-stole-BIG-IP-source-code
*   [3] Inside the F5 Breach: What We Know and Recommended Actions. (2025, October 16). Rapid7. Truy cập từ: https://www.rapid7.com/blog/post/ve-inside-the-f5-breach-what-we-know-and-recommended-actions/
*   [4] F5 Breach Exposes BIG-IP Source Code. (2025, October 15). The Hacker News. Truy cập từ: https://thehackernews.com/2025/10/f5-breach-exposes-big-ip-source-code.html
*   [5] Frequently Asked Questions About the August 2025 F5 Security Incident. (2025, October 15). Tenable. Truy cập từ: https://www.tenable.com/blog/frequently-asked-questions-about-the-august-2025-f5-security-incident
*   [6] Alert - AL25-014 Security Incident impacting F5. (2025, October 15). Canadian Centre for Cyber Security. Truy cập từ: https://www.cyber.gc.ca/en/alerts-advisories/al25-014-security-incident-impacting-f5
*   [7] Multiple high-severity vulnerabilities in F5 products and incident impacting F5. (2025, October 15). Australian Cyber Security Centre. Truy cập từ: https://www.cyber.gov.au/alerts-and-advisories/2025-10-15-multiple-high-severity-vulnerabilities-f5-products-and-incident-impacting-f5
*   [8] F5 Confirms Breach of Internal Systems—Source Code, Customer ... (2025, October 15). Picus Security. Truy cập từ: https://www.picussecurity.com/resource/blog/f5-confirms-breach-of-internal-systems
*   [9] K000154696: F5 Security Incident. (2025, October 15). F5. Truy cập từ: https://my.f5.com/manage/s/article/K000154696
*   [10] F5 Security Incident Advisory. (2025, October 15). Zscaler. Truy cập từ: https://www.zscaler.com/blogs/security-research/f5-security-incident-advisory
*   [11] CVE-2025-53868: F5 BIG-IP Appliance Mode Bypass. (2025, October 15). ZeroPath. Truy cập từ: https://zeropath.com/blog/cve-2025-53868-f5-big-ip-appliance-mode-bypass
*   [12] CVE-2025-53868 F5 BIG-IP Appliance Mode Bypass Vulnerability. (2025, October 15). Wiz.io. Truy cập từ: https://www.wiz.io/vulnerability-database/cve/cve-2025-53868
*   [13] CVE-2025-61955: F5OS Privilege Escalation Summary. (2025, October 15). ZeroPath. Truy cập từ: https://zeropath.com/blog/cve-2025-61955-f5os-privilege-escalation-summary
*   [14] K000151902: F5OS Privilege Escalation Vulnerability. (2025, October 15). F5. Truy cập từ: https://my.f5.com/manage/s/article/K000151902