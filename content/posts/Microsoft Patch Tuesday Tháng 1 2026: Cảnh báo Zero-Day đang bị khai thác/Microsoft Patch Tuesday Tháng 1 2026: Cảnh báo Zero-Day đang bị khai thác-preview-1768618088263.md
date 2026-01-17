---
title: "Microsoft Patch Tuesday Tháng 1 2026: Cảnh báo Zero-Day đang bị khai thác"
date: 2026-01-17T07:01:46.874+07:00
draft: false
tags: ["An ninh mạng", "Bảo mật hệ thống", "Lỗ hổng bảo mật", "Tấn công mạng", "Phòng thủ mạng", "Endpoint Security", "XDR", "Threat Intelligence"]
categories: ["Cyber Security"]
---

### Mở đầu

Bản vá Patch Tuesday tháng 1 năm 2026 của Microsoft đã mang đến một khởi đầu đầy thách thức cho các chuyên gia an ninh mạng. Bản cập nhật này không chỉ khắc phục số lượng lớn các lỗ hổng mà còn đặc biệt cảnh báo về ba lỗ hổng zero-day, trong đó có một lỗ hổng đang bị tin tặc khai thác tích cực. Điều này một lần nữa nhấn mạnh sự cấp bách của việc duy trì các bản vá bảo mật và sự cảnh giác liên tục trước các mối đe dọa mới.

![Microsoft Patch Tuesday Tháng 1 2026](Microsoft-Patch-Tuesday-January-2026-scaled.png)

### Tổng quan Microsoft Patch Tuesday Tháng 1 2026

Bản vá tháng 1/2026 của Microsoft đã khắc phục tổng cộng **113 lỗ hổng** bảo mật mới [1, 2, 4, 5]. Trong số này, có **9 lỗ hổng được đánh giá là Critical (nghiêm trọng)**, và phần lớn còn lại là Important (quan trọng) [1, 2].

Điểm nổi bật nhất là sự xuất hiện của **ba lỗ hổng zero-day**, tức là các lỗ hổng đã được tin tặc biết đến và có thể đã bị khai thác trước khi Microsoft phát hành bản vá. Một trong số đó (CVE-2026-20805) được xác nhận là đang bị khai thác tích cực trong môi trường thực tế [1, 3, 5].

### CVE-2026-20805: Lỗ hổng Zero-Day trong Desktop Window Manager (DWM) bị khai thác

Lỗ hổng nghiêm trọng nhất trong đợt này là **CVE-2026-20805**, liên quan đến **Desktop Window Manager (DWM)** của Windows [3, 5].

*   **Mô tả**: Đây là một lỗ hổng Information Disclosure (tiết lộ thông tin) với điểm CVSS 5.5, được xếp hạng Important [3]. Mặc dù không trực tiếp dẫn đến việc thực thi mã từ xa, nhưng nó cho phép kẻ tấn công đã được xác thực cục bộ tiết lộ các thông tin nhạy cảm từ bộ nhớ user-mode, chẳng hạn như địa chỉ phân đoạn (section addresses) từ cổng ALPC [3, 5].
*   **Tác động**: Việc tiết lộ thông tin này có thể bị lạm dụng để hỗ trợ các cuộc tấn công leo thang đặc quyền (Elevation of Privilege) hoặc thực thi mã từ xa, bằng cách cung cấp dữ liệu cần thiết để vượt qua các biện pháp bảo vệ hệ thống như ASLR (Address Space Layout Randomization) [3, 5].
*   **Tình trạng khai thác**: Đáng báo động là lỗ hổng này đã bị **khai thác tích cực trong thực tế** [1, 3]. Điều này có nghĩa là các hệ thống chưa được vá có nguy cơ rất cao bị tấn công. Lỗ hổng này cũng đã được CISA thêm vào danh mục các lỗ hổng đã bị khai thác (KEV Catalog) [6].
*   **Sản phẩm bị ảnh hưởng**: Rất nhiều phiên bản của hệ điều hành Windows bị ảnh hưởng, bao gồm Windows 10, Windows 11 và các phiên bản Windows Server từ 2012 đến 2025 [3].
*   **Giải pháp**: Microsoft đã phát hành các bản cập nhật bảo mật cụ thể (ví dụ: KB5074109, KB5073450) để khắc phục CVE-2026-20805. Việc áp dụng các bản vá này là cực kỳ cấp bách [3].

### Các lỗ hổng Zero-Day đáng chú ý khác

Bên cạnh CVE-2026-20805, bản vá tháng 1/2026 còn bao gồm hai lỗ hổng zero-day khác đã được công khai:

*   **CVE-2026-21265 (Windows Secure Boot)**: Đây là lỗ hổng bỏ qua tính năng bảo mật do hết hạn chứng chỉ Secure Boot (Secure Boot Certificate Expiration Security Feature Bypass) với điểm CVSS 6.4 (hoặc 5.6) [10]. Lỗ hổng này xuất phát từ việc các chứng chỉ Secure Boot ban đầu của Microsoft sắp hết hạn, có thể làm gián đoạn chuỗi tin cậy của Secure Boot nếu không được cập nhật. Mặc dù đã được công khai, hiện chưa có thông tin về việc lỗ hổng này bị khai thác tích cực [10].
*   **CVE-2026-20876 (Windows VBS Enclave)**: Đây là lỗ hổng leo thang đặc quyền (Elevation of Privilege) loại use-after-free trong Windows VBS Enclave, được đánh giá là Critical. Lỗ hổng này cũng đã được công khai nhưng không có bằng chứng về việc bị khai thác tích cực [2].

### Các thành phần và dịch vụ khác bị ảnh hưởng

Patch Tuesday tháng 1/2026 bao phủ một loạt các sản phẩm và thành phần của Microsoft, bao gồm:

*   **Windows Kernel, NTLM, RPC**: Các lỗ hổng liên quan đến leo thang đặc quyền và tiết lộ thông tin.
*   **Microsoft Office**: Các lỗ hổng thực thi mã từ xa (RCE) tiềm ẩn. Đáng chú ý là các lỗi RCE nghiêm trọng trong Microsoft Office (CVE-2026-20952 và CVE-2026-20953) với điểm CVSS 8.4, có thể bị khai thác thông qua các tài liệu độc hại [6, 9].
*   **SharePoint**: Các lỗ hổng bảo mật có thể ảnh hưởng đến các môi trường cộng tác doanh nghiệp.
*   **Windows NTFS, Graphics Kernel**: Các thành phần cốt lõi của hệ điều hành.

### Khuyến nghị và Giải pháp

Với sự xuất hiện của lỗ hổng zero-day đang bị khai thác tích cực, việc cập nhật bảo mật trở nên cấp thiết hơn bao giờ hết.

*   **Ưu tiên Cập nhật ngay lập tức**: Các tổ chức và người dùng cần ưu tiên triển khai các bản vá bảo mật của Microsoft cho tháng 1/2026 ngay lập tức. Đặc biệt chú ý đến các hệ thống chạy DWM, Windows Secure Boot, Windows VBS Enclave và các sản phẩm Office.
*   **Quản lý bản vá**: Xây dựng và duy trì quy trình quản lý bản vá hiệu quả, tự động hóa nếu có thể, để đảm bảo tất cả các hệ thống đều được cập nhật kịp thời.
*   **Nguyên tắc đặc quyền tối thiểu (Least Privilege)**: Hạn chế tối đa các đặc quyền của người dùng và ứng dụng để giảm thiểu tác động nếu một cuộc tấn công thành công.
*   **Giải pháp EDR/XDR**: Triển khai các giải pháp Endpoint Detection and Response (EDR) hoặc Extended Detection and Response (XDR) để phát hiện và phản ứng nhanh chóng với các hoạt động độc hại, đặc biệt là các cuộc tấn công zero-day.
*   **Phân đoạn mạng (Network Segmentation)**: Giảm thiểu khả năng lây lan của các cuộc tấn công bằng cách phân đoạn mạng, cô lập các hệ thống quan trọng.
*   **Sao lưu dữ liệu**: Thường xuyên sao lưu dữ liệu quan trọng và đảm bảo các bản sao lưu được bảo vệ an toàn.

### Kết luận

Bản vá Microsoft Patch Tuesday tháng 1/2026 đã đưa ra một lời cảnh báo rõ ràng về bối cảnh mối đe dọa đang phát triển. Sự tồn tại của các lỗ hổng zero-day, đặc biệt là CVE-2026-20805 đang bị khai thác tích cực, càng nhấn mạnh tầm quan trọng của việc cập nhật bảo mật liên tục và chủ động. Bằng cách ưu tiên vá lỗi và áp dụng các biện pháp an ninh mạng mạnh mẽ, các tổ chức có thể bảo vệ hệ thống của mình trước những rủi ro ngày càng tăng.

### Nguồn tham khảo

*   [1] CrowdStrike Blog: https://www.crowdstrike.com/en-us/blog/patch-tuesday-analysis-january-2026/
*   [2] Qualys Blog: https://blog.qualys.com/vulnerabilities-threat-research/2026/01/13/microsoft-patch-tuesday-january-2026-security-update-review
*   [3] Tenable Blog: https://www.tenable.com/blog/microsofts-january-2026-patch-tuesday-addresses-113-cves-cve-2026-20805
*   [4] Lansweeper Blog: https://www.lansweeper.com/blog/patch-tuesday/microsoft-patch-tuesday-january-2026/
*   [5] Arctic Wolf Blog: https://arcticwolf.com/resources/blog/microsoft-patch-tuesday-january-2026/
*   [6] CISA Adds Microsoft Windows Vulnerability CVE-2026-20805 to KEV Catalog: https://www.scworld.com/brief/cisa-adds-microsoft-windows-vulnerability-cve-2026-20805-to-kev-catalog
*   [7] Krebs on Security: https://krebsonsecurity.com/2026/01/patch-tuesday-january-2026-edition/
*   [8] SANS ISC: https://isc.sans.edu/diary/January+2026+Microsoft+Patch+Tuesday+Summary/32624
*   [9] The Stack Technology: https://www.thestack.technology/patch-tuesday-2026s-first-0day-and-office-at-high-risk/
*   [10] Rapid7 Vulnerability Database: https://www.rapid7.com/db/vulnerabilities/microsoft-windows-cve-2026-21265/
