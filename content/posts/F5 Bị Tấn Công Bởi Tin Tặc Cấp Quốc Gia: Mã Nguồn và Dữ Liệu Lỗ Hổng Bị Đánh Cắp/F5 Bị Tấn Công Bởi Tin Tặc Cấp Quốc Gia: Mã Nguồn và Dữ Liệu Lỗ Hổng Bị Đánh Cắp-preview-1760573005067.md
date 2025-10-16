---
title: "F5 Bị Tấn Công Bởi Tin Tặc Cấp Quốc Gia: Mã Nguồn và Dữ Liệu Lỗ Hổng Bị Đánh Cắp"
date: 2025-10-16T07:02:45.124+07:00
draft: false
tags: ["An ninh mạng", "Bảo mật hệ thống", "Lỗ hổng bảo mật", "Tấn công mạng", "Phòng thủ mạng", "Quản lý rủi ro", "Giám sát bảo mật"]
categories: ["Cyber Security"]
---

Vào tháng 8 năm 2025, F5, một trong những nhà cung cấp giải pháp mạng và bảo mật hàng đầu thế giới, đã trở thành nạn nhân của một vụ tấn công mạng tinh vi được cho là do các tác nhân cấp quốc gia thực hiện. Vụ việc nghiêm trọng này đã dẫn đến việc đánh cắp mã nguồn của sản phẩm BIG-IP cùng với dữ liệu về các lỗ hổng bảo mật chưa được công bố. Sự kiện này không chỉ gây chấn động trong cộng đồng an ninh mạng mà còn thúc đẩy Cơ quan An ninh Cơ sở hạ tầng và An ninh mạng Hoa Kỳ (CISA) phải ban hành các chỉ thị khẩn cấp, nhấn mạnh mức độ rủi ro và cần thiết phải có hành động kịp thời [3, 5, 6].

![F5 Bị Tấn Công Bởi Tin Tặc Cấp Quốc Gia: Mã Nguồn và Dữ Liệu Lỗ Hổng Bị Đánh Cắp](/images/2025/F5 Bị Tấn Công Bởi Tin Tặc Cấp Quốc Gia: Mã Nguồn và Dữ Liệu Lỗ Hổng Bị Đánh Cắp/F5-headpic.jpg)

### Bối cảnh vụ tấn công

Vào ngày 9 tháng 8 năm 2025, F5 đã phát hiện ra rằng một tác nhân đe dọa cấp quốc gia đã giành được quyền truy cập trái phép vào một số hệ thống nội bộ của họ. Các hệ thống bị ảnh hưởng bao gồm môi trường phát triển BIG-IP và các nền tảng kiến thức kỹ thuật [2, 7, 11]. Ngay lập tức, F5 đã kích hoạt quy trình ứng phó sự cố, hợp tác với các chuyên gia an ninh mạng hàng đầu như CrowdStrike và Mandiant, đồng thời báo cáo vụ việc cho các cơ quan thực thi pháp luật Hoa Kỳ và SEC [2, 7, 3]. F5 cũng được Bộ Tư pháp Hoa Kỳ cho phép trì hoãn việc công bố rộng rãi do "rủi ro đáng kể đối với an ninh quốc gia hoặc an toàn công cộng" [3, 5].

### Kẻ tấn công và Phương thức xâm nhập

Những kẻ tấn công đã duy trì quyền truy cập dai dẳng vào các hệ thống phát triển và kỹ thuật sản phẩm liên quan đến BIG-IP. Mục tiêu chính của chúng là tải xuống mã nguồn và dữ liệu về các lỗ hổng chưa được tiết lộ [2, 7, 5, 11]. F5 báo cáo rằng không có sự xâm phạm nào đối với các môi trường tài chính, CRM, NGINX, F5 Distributed Cloud, Silverline hoặc các môi trường đám mây khác của họ [2, 9, 11]. Điều này cho thấy mục tiêu cụ thể của vụ tấn công là thu thập thông tin độc quyền về sản phẩm cốt lõi của F5.

### Phạm vi dữ liệu bị đánh cắp

Dữ liệu bị đánh cắp bao gồm:
*   **Mã nguồn BIG-IP và các tài liệu kỹ thuật,** bao gồm một số dữ liệu về các lỗ hổng chưa được công bố [2, 11].
*   Một số tệp chứa **dữ liệu cấu hình khách hàng hạn chế**, nhưng không phải hồ sơ khách hàng rộng rãi [2, 11].

F5 khẳng định các đánh giá độc lập không tìm thấy bằng chứng về việc chuỗi cung ứng hoặc hệ thống xây dựng phần mềm bị giả mạo [2, 11].

### Phản ứng của F5

Sau khi phát hiện vụ việc, F5 đã thực hiện một loạt các biện pháp ứng phó toàn diện:

*   **Cô lập:** Các hệ thống bị ảnh hưởng đã được cô lập, và F5 không tìm thấy bằng chứng về hoạt động trái phép tiếp theo [2, 11].
*   **Tăng cường bảo mật:** F5 đã xoay vòng thông tin đăng nhập, thắt chặt kiểm soát truy cập, tăng cường giám sát và vá lỗi, đồng thời cải thiện phân đoạn mạng [2, 11].
*   **Hỗ trợ bên ngoài:** F5 đã hợp tác với CrowdStrike, Mandiant, NCC Group và IOActive để đánh giá sự cố, triển khai EDR (Endpoint Detection and Response) và kiểm tra mã sản phẩm [2, 7, 11].
*   **Tiếp cận khách hàng:** F5 đã thông báo cho các khách hàng bị ảnh hưởng và cung cấp đăng ký Falcon EDR miễn phí để tăng cường khả năng phòng thủ của BIG-IP [2, 11].
*   **Phát hành bản vá:** F5 đã phát hành các bản cập nhật và bản vá để khắc phục các lỗ hổng được xác định là có nguy cơ do dữ liệu bị đánh cắp [1, 11].

### Khuyến nghị của CISA

Đáp lại vụ việc, CISA đã ban hành một chỉ thị khẩn cấp, hướng dẫn các nhà điều hành hạ tầng liên bang và cơ sở hạ tầng quan trọng phải:

*   **Áp dụng ngay lập tức tất cả các bản cập nhật và bản vá bảo mật F5 BIG-IP** [3].
*   **Tăng cường giám sát** các dấu hiệu xâm nhập trên môi trường F5 [3].
*   **Xem xét nhật ký truy cập và kiểm toán** để tìm kiếm hoạt động đáng ngờ [3].
*   **Vô hiệu hóa việc phơi bày giao diện quản lý không cần thiết ra internet** [3].

CISA nhấn mạnh mối đe dọa liên tục về việc khai thác các thiết bị F5 BIG-IP chưa được vá, nhắc đến CVE-2022-1388 và các vấn đề tương tự trong quá khứ [10].

### Tác động và Bài học

Vụ tấn công F5 là một lời nhắc nhở rõ ràng về sự nguy hiểm của các tác nhân cấp quốc gia và tầm quan trọng của việc bảo vệ chuỗi cung ứng phần mềm. Việc mã nguồn và dữ liệu lỗ hổng chưa được công bố bị đánh cắp có thể mang lại lợi thế đáng kể cho kẻ tấn công, cho phép chúng phát triển các cuộc tấn công tinh vi hơn nhắm vào các tổ chức sử dụng sản phẩm F5 BIG-IP.

Các tổ chức cần:
*   **Thường xuyên cập nhật và vá lỗi** các hệ thống F5 BIG-IP.
*   **Triển khai giám sát nâng cao** trên các thiết bị F5 và môi trường liên quan.
*   **Thực hiện kiểm soát truy cập nghiêm ngặt** và phân đoạn mạng.
*   **Đào tạo nhân viên** về các mối đe dọa mới nhất và các biện pháp phòng ngừa.

### Kết luận

Vụ tấn công vào F5 bởi tin tặc cấp quốc gia, với việc đánh cắp mã nguồn và dữ liệu lỗ hổng của BIG-IP, là một sự cố nghiêm trọng đòi hỏi sự chú ý cao độ từ các tổ chức trên toàn cầu. Phản ứng nhanh chóng của F5 cùng với các khuyến nghị từ CISA cung cấp một lộ trình rõ ràng để giảm thiểu rủi ro. Tuy nhiên, bài học lớn nhất là sự cần thiết phải liên tục cảnh giác, đầu tư vào an ninh mạng mạnh mẽ và chuẩn bị sẵn sàng cho những mối đe dọa ngày càng tinh vi từ các tác nhân có khả năng cao.

---

### Nguồn tham khảo:
[1] F5 releases BIG-IP patches for stolen security vulnerabilities. (2025, October 15). BleepingComputer.
[2] A sophisticated nation-state actor breached F5 systems, stealing BIG ... (2025, October 15). Security Affairs.
[3] CISA issues emergency directive after F5 discloses nation-state breach. (n.d.). SC Media.
[4] UK National Cyber Security Centre. (n.d.).
[5] F5 BIG-IP Environment Breached by Nation-State Actor. (2025, October 15). Dark Reading.
[6] TechCrunch. (2025, October 15). Cyber giant F5 Networks says government hackers had long-term access to its systems, stole code and customer data.
[7] F5 discloses major security breach linked to nation-state hackers. (n.d.). GeekWire.
[8] MyF5. (n.d.). K000154696: F5 Security Incident - MyF5 | Support.
[9] K000154696: F5 Security Incident - MyF5 | Support. (n.d.). MyF5.
[10] Threat Actors Exploiting F5 BIG-IP CVE-2022-1388 | AHA. (n.d.). AHA.
[11] FAQ on F5 Security Incident - Blog | Tenable®. (2025, October 15). Tenable.