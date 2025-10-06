---
title: "Broadcom Vá Lỗ Hổng Zero-Day Trong VMware Bị UNC5174 Khai Thác"
date: 2025-10-05T07:02:57.268+07:00
draft: false
tags: ["An ninh mạng", "Bảo mật hệ thống", "Lỗ hổng bảo mật", "Tấn công mạng", "Phòng thủ mạng", "Quản lý rủi ro", "Giám sát bảo mật", "Threat Intelligence"]
categories: ["Cyber Security"]
---

![Hình ảnh minh họa: UNC5174 khai thác lỗ hổng CVE-2025-41244 của VMware để chiếm quyền root.](/image/2025/Broadcom%20V%C3%A1%20L%E1%BB%97%20H%E1%BB%95ng%20Zero-Day%20Trong%20VMware%20B%E1%BB%8B%20UNC5174%20Khai%20Th%C3%A1c/unc5174-weaponizes-vmware-cve-2025-41244-bug-for-privilege-escalation.webp)

Trong bối cảnh mối đe dọa an ninh mạng ngày càng tinh vi, việc một lỗ hổng zero-day bị khai thác trong các hệ thống quan trọng như VMware luôn gây ra báo động cao. Gần đây, Broadcom đã phát hành bản vá cho CVE-2025-41244, một lỗ hổng leo thang đặc quyền cục bộ (Local Privilege Escalation - LPE) trong VMware Aria Operations và VMware Tools. Lỗ hổng này đã bị nhóm tấn công có liên kết với Trung Quốc, UNC5174, tích cực khai thác từ giữa tháng 10 năm 2024, gây ra rủi ro nghiêm trọng cho các môi trường ảo hóa trên toàn cầu.

## CVE-2025-41244: Lỗ Hổng Leo Thang Đặc Quyền Cục Bộ

CVE-2025-41244 là một lỗ hổng leo thang đặc quyền cục bộ cho phép người dùng không có đặc quyền trên một máy ảo có thể chiếm quyền root (quản trị viên cao nhất) trên hệ thống bị ảnh hưởng [1, 2, 3, 4].

### Bản chất và Cơ chế khai thác

*   **Bản chất:** Lỗ hổng này phát sinh từ việc xử lý đặc quyền không đúng cách trong các môi trường mà VMware Aria Operations quản lý các máy ảo được trang bị VMware Tools và gói quản lý Service Discovery Management Pack (SDMP) được bật [1, 2].
*   **Cơ chế khai thác:** Lỗ hổng liên quan đến một định nghĩa đặc quyền không an toàn (unsafe privilege definition) và đường dẫn tìm kiếm không đáng tin cậy (untrusted search path), được phân loại theo CWE-267 và CWE-426. Cụ thể:
    *   Một script (`get-versions.sh`) trong SDMP sử dụng các mẫu biểu thức chính quy (regex patterns) quá rộng để định vị các tệp nhị phân của dịch vụ.
    *   Kẻ tấn công có quyền truy cập cục bộ, không phải quản trị viên, có thể đặt một tệp nhị phân độc hại (ví dụ: `/tmp/httpd`) vào một đường dẫn có thể ghi.
    *   Khi chức năng khám phá dịch vụ được thực thi, nó sẽ chạy tệp nhị phân độc hại này với quyền root, cấp cho kẻ tấn công toàn quyền kiểm soát hệ thống [2, 3].
*   **Các thành phần bị ảnh hưởng:** Lỗ hổng này ảnh hưởng đến cả chế độ khám phá *không cần thông tin đăng nhập* (qua VMware Tools trên các VM khách) và chế độ *dựa trên thông tin đăng nhập cũ* (qua Aria Operations). Vấn đề cũng đã được xác nhận trong `open-vm-tools` trên Linux [2].
*   **Hậu quả:** Sau khi khai thác thành công, kẻ tấn công có thể cài đặt chương trình, sửa đổi hoặc xóa dữ liệu, hoặc tạo tài khoản với quyền root trên máy ảo bị ảnh hưởng [1, 3, 4].

## Nhóm Tấn Công UNC5174

UNC5174 được xác định là một nhóm tấn công tinh vi, được cho là có **liên kết với Trung Quốc và được nhà nước bảo trợ** [3, 4].

*   Nhóm này đã **tích cực khai thác** CVE-2025-41244 như một lỗ hổng zero-day từ giữa tháng 10 năm 2024.
*   Theo các nhà nghiên cứu tại NVISO Labs và nhiều thông báo bảo mật, UNC5174 là tác nhân duy nhất được xác nhận đã khai thác lỗ hổng này tính đến đầu tháng 10 năm 2025 [3, 4].

## Tác động và Rủi ro

*   Lỗ hổng này có **điểm CVSS cơ bản là 7.8 (Cao)** [2].
*   Nó cho phép **leo thang đặc quyền hoàn toàn** từ bất kỳ người dùng không có đặc quyền nào lên quyền root, biến nó thành một rủi ro nghiêm trọng đối với các doanh nghiệp, chính phủ và bất kỳ tổ chức nào sử dụng các triển khai VMware bị ảnh hưởng [4].
*   **Khả năng ảnh hưởng rộng rãi:** Do việc sử dụng phổ biến VMware trong cơ sở hạ tầng doanh nghiệp và chính phủ, lỗ hổng này có tiềm năng ảnh hưởng đến một lượng lớn hệ thống trên toàn cầu [1, 3, 4].

## Quy trình công bố của Broadcom

*   **Broadcom** (công ty mẹ hiện tại của VMware) đã chính thức **công bố** CVE-2025-41244 thông qua một bản tư vấn bảo mật sau khi nhận được thông báo tiết lộ có trách nhiệm từ NVISO Labs [3].
*   Bản tư vấn đã mô tả lỗ hổng, làm rõ các yêu cầu khai thác (quyền truy cập cục bộ không phải quản trị viên, SDMP được bật) và liệt kê tất cả các sản phẩm và phiên bản bị ảnh hưởng [3].
*   Phản ứng của Broadcom bao gồm:
    *   **Thông báo công khai ngay lập tức** sau khi việc khai thác trong thực tế được xác nhận.
    *   **Phối hợp với các nhà nghiên cứu bảo mật**, cung cấp cả các bước khắc phục kỹ thuật và bản vá phiên bản.
    *   **Các bản vá và biện pháp giảm thiểu chính thức** đã được phát hành cho tất cả các phiên bản cốt lõi bị ảnh hưởng (ví dụ: VMware Tools 13.0.5, Aria Operations 8.18.5) [3].
*   Các bản tư vấn bảo mật của các cơ quan chính phủ (ví dụ: MS-ISAC) đã lặp lại hướng dẫn của Broadcom, khẳng định rằng CVE-2025-41244 đã được xử lý kịp thời ngay sau khi việc khai thác được báo cáo [4].

## Bảng tóm tắt các phiên bản bị ảnh hưởng và đã sửa lỗi

| Sản phẩm                                 | Phiên bản bị ảnh hưởng           | Phiên bản đã sửa lỗi      |
| :--------------------------------------- | :----------------------------- | :------------------ |
| VMware Tools                            | < 13.0.5 / 12.5.4         | 13.0.5 / 12.5.4    |
| VMware Aria Operations                  | < 8.18.5                   | 8.18.5             |
| VMware Cloud Foundation Operations       | < 9.0.1.0                  | 9.0.1.0            |

## Lời khuyên phát hiện chính

*   Giám sát các tiến trình bất thường được tạo ra bởi `vmtoolsd` hoặc `get-versions.sh`.
*   Theo dõi sự hiện diện của các tệp nhị phân đáng ngờ trong các thư mục có thể ghi được bởi mọi người dùng (world-writable directories) như `/tmp` [2].

## Kết luận

CVE-2025-41244 vẫn là một mối lo ngại nghiêm trọng do tính dễ khai thác, khả năng cung cấp quyền truy cập cấp root và khả năng đã được chứng minh cùng hoạt động của các tác nhân đe dọa tinh vi, được nhà nước bảo trợ như UNC5174 trong việc tận dụng nó. Các tổ chức được khuyến nghị khẩn trương áp dụng các bản vá và biện pháp giảm thiểu được Broadcom cung cấp để bảo vệ môi trường ảo hóa của mình khỏi các cuộc tấn công tiềm tàng.

## Trích dẫn nguồn

*   [1] Zeropath security summary: [https://zeropath.com/blog/cve-2025-41244-vmware-aria-operations-tools-lpe-summary](https://zeropath.com/blog/cve-2025-41244-vmware-aria-operations-tools-lpe-summary)
*   [2] SOC Prime detailed analysis: [https://socprime.com/blog/cve-2025-41244-zero-day-vulnerability/](https://socprime.com/blog/cve-2025-41244-zero-day-vulnerability/)
*   [3] Qualys and Broadcom advisories: [https://threatprotect.qualys.com/2025/10/01/broadcom-addresses-actively-exploited-vulnerability-in-vmware-aria-operations-and-vmware-tools-cve-2025-41244/](https://threatprotect.qualys.com/2025/10/01/broadcom-addresses-actively-exploited-vulnerability-in-vmware-aria-operations-and-vmware-tools-cve-2025-41244/)
*   [4] MS-ISAC government security advisory: [https://www.cisecurity.org/advisory/multiple-vulnerabilities-in-vmware-aria-operations-and-vmware-tools-could-allow-for-privilege-escalation_2025-092](https://www.cisecurity.org/advisory/multiple-vulnerabilities-in-vmware-aria-operations-and-vmware-tools-could-allow-for-privilege-escalation_2025-092)
