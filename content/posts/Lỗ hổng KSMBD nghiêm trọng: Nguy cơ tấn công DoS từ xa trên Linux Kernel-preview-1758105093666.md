---
title: "Lỗ hổng KSMBD nghiêm trọng: Nguy cơ tấn công DoS từ xa trên Linux Kernel"
date: 2025-09-17T17:26:00.417+07:00
draft: false
tags: ["KSMBD", "DoS", "CVE-2025-38501", "SMB", "lỗ hổng", "tấn công từ xa", "kernel 5.3", "vulnerability", "patch", "Linux"]
categories: ["Cyber Security", "Software Tool"]
---

## Lỗ hổng KSMBD nghiêm trọng: Nguy cơ tấn công DoS từ xa trên Linux Kernel

Lỗ hổng bảo mật luôn là mối quan tâm hàng đầu trong thế giới công nghệ, đặc biệt là khi chúng ảnh hưởng đến các thành phần cốt lõi của hệ điều hành. Gần đây, một lỗ hổng nghiêm trọng được gán mã **CVE-2025-38501** đã được phát hiện trong triển khai máy chủ SMB KSMBD của Linux kernel, cho phép kẻ tấn công từ xa thực hiện tấn công Từ chối Dịch vụ (DoS) [1, 3, 5]. Bài viết này sẽ đi sâu vào chi tiết của lỗ hổng này, tác động của nó và các biện pháp khắc phục cần thiết.

![Lỗ hổng KSMBD nghiêm trọng trên Linux Kernel](/images/2025/Linux-Kernel-CVE-2025-37899-1024x614.png)

### KSMBD là gì?

KSMBD là một máy chủ tệp SMB (Server Message Block) trong nhân Linux, được giới thiệu từ phiên bản Linux kernel 5.3 trở lên [1, 2, 3]. Chức năng chính của KSMBD là cung cấp khả năng chia sẻ tệp qua mạng, cho phép các hệ thống Linux hoạt động như một máy chủ tệp tương thích với giao thức SMB3. Việc tích hợp SMB trực tiếp vào kernel giúp cải thiện hiệu suất và độ ổn định so với các giải pháp SMB dựa trên không gian người dùng truyền thống như Samba [2].

### Chi tiết về Lỗ hổng CVE-2025-38501

Lỗ hổng **CVE-2025-38501** là một lỗi trong cách KSMBD quản lý các kết nối, cho phép kẻ tấn công từ xa làm cạn kiệt tài nguyên kết nối của máy chủ, dẫn đến tình trạng từ chối dịch vụ [1, 2, 3, 5].

#### Tổng quan và Chi tiết kỹ thuật

Lỗ hổng này được kích hoạt khi một kẻ tấn công từ xa hoàn thành quá trình bắt tay TCP ban đầu nhưng sau đó ngừng phản hồi các gói tin tiếp theo. Điều này khiến máy chủ giữ các kết nối này mở vô thời hạn [1, 2, 3].

*   **Cách thức hoạt động:** Kẻ tấn công có thể sử dụng các tài nguyên tối thiểu để liên tục tạo các kết nối TCP và ngừng giao tiếp sau bắt tay, buộc máy chủ KSMBD duy trì trạng thái chờ.
*   **Tiêu thụ tài nguyên:** Kẻ tấn công có thể tiêu thụ một cách có hệ thống tất cả các khe kết nối có sẵn, ngăn chặn người dùng hợp pháp truy cập vào các dịch vụ SMB [1, 2, 3].
*   **Khả năng khai thác:** Ngay cả khi các cấu hình thời gian chờ tùy chỉnh được thiết lập, thời gian chờ tối thiểu (1 phút) vẫn đủ để kẻ tấn công lặp lại các cuộc tấn công, làm cho lỗ hổng này dễ bị khai thác từ xa và không yêu cầu xác thực [1, 2, 3].

#### Tác động

*   **Các phiên bản bị ảnh hưởng:** Tất cả các phiên bản Linux kernel từ 5.3 trở đi đang chạy máy chủ KSMBD SMB đều bị ảnh hưởng [1, 2, 3].
*   **Hệ thống có nguy cơ:** Bất kỳ hệ thống nào cung cấp dịch vụ SMB/CIFS thông qua KSMBD đều có nguy cơ, bao gồm máy chủ tệp, thiết bị NAS (Network Attached Storage) và các triển khai cấp doanh nghiệp [1, 2, 3].
*   **Vector tấn công:** Cuộc tấn công dựa trên mạng và có thể được khởi động bởi bất kỳ kẻ thù từ xa không cần xác thực nào [5]. Hậu quả trực tiếp là người dùng hợp pháp không thể truy cập tài nguyên chia sẻ, gây gián đoạn hoạt động kinh doanh.

### Biện pháp khắc phục và giảm thiểu

Để bảo vệ hệ thống khỏi lỗ hổng CVE-2025-38501, các quản trị viên hệ thống cần thực hiện các bước sau:

*   **Cập nhật Kernel:** Lỗ hổng này đã được khắc phục trong commit `e6bb9193974059ddbb0ce7763fa3882bd60d4dc3` của Linux kernel, giúp sửa đổi việc quản lý kết nối của KSMBD [1, 2, 3]. Quản trị viên hệ thống nên cập nhật lên phiên bản kernel đã được vá càng sớm càng tốt.
*   **Xem xét cấu hình SMB:** Rà soát và cấu hình lại các giới hạn kết nối và thời gian chờ nghiêm ngặt cho dịch vụ SMB như một biện pháp phòng thủ bổ sung [2, 3]. Điều này có thể giúp hạn chế số lượng kết nối tối đa mà một máy chủ KSMBD có thể xử lý, giảm thiểu tác động của một cuộc tấn công DoS.

### Bảng tóm tắt CVE-2025-38501

| Thuộc tính | Chi tiết |
| :--- | :--- |
| **CVE ID** | CVE-2025-38501 |
| **Loại lỗ hổng** | Từ chối Dịch vụ (DoS) |
| **Sản phẩm bị ảnh hưởng** | Linux Kernel KSMBD (phiên bản 5.3 trở lên) |
| **Vector tấn công** | Từ xa, qua mạng |
| **Xác thực** | Không yêu cầu (không xác thực) |
| **Đã sửa trong** | Commit e6bb9193974059ddbb0ce7763fa3882bd60d4dc3 |
| **Biện pháp giảm thiểu** | Cập nhật kernel, cấu hình giới hạn kết nối và thời gian chờ SMB |

### Kết luận

Lỗ hổng CVE-2025-38501 trong KSMBD của Linux kernel là một mối đe dọa nghiêm trọng đối với bất kỳ hệ thống nào sử dụng dịch vụ SMB/CIFS thông qua KSMBD. Khả năng thực hiện tấn công DoS từ xa mà không cần xác thực làm cho nó trở thành mục tiêu hấp dẫn cho kẻ tấn công. Việc cập nhật kernel lên phiên bản đã vá và rà soát cấu hình SMB là những bước quan trọng và cần thiết để bảo vệ hệ thống của bạn khỏi nguy cơ này. Hãy luôn ưu tiên cập nhật bảo mật để duy trì sự an toàn và ổn định cho hạ tầng của bạn.

### Nguồn tham khảo

*   [1] [Linux Kernel KSMBD Flaw Lets Remote Attackers Drain Server ...](https://gbhackers.com/linux-kernel-ksmbd-flaw/)
*   [2] [Linux Kernel KSMBD NULL Pointer Dereference Vulnerability](https://www.sonicwall.com/blog/linux-kernel-ksmbd-null-pointer-dereference-vulnerability)
*   [3] [KSMBDrain (CVE-2025-38501) Linux Kernel Flaw Allows Remote DoS Attacks (PoC Available) - SecurityOnline.info](https://securityonline.info/ksmbdrain-cve-2025-38501-linux-kernel-flaw-allows-remote-dos-attacks-poc-available/)
*   [4] [oss-security - [CVE-2025-38501] Linux kernel: KSMBD service DoS ...](https://www.openwall.com/lists/oss-security/2025/09/15/2)
*   [5] [CVE-2025-38501 Detail](https://nvd.nist.gov/vuln/detail/CVE-2025-38501)