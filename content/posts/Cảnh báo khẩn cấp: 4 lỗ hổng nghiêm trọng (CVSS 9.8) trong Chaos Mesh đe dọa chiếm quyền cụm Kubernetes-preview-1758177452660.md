---
title: "Cảnh báo khẩn cấp: 4 lỗ hổng nghiêm trọng (CVSS 9.8) trong Chaos Mesh đe dọa chiếm quyền cụm Kubernetes"
date: 2025-09-18T13:35:49.841+07:00
draft: false
tags: ["An ninh mạng", "Bảo mật hệ thống", "Lỗ hổng bảo mật", "Tấn công mạng", "Quản lý rủi ro", "Kubernetes", "Container", "Hạ tầng đám mây", "DevOps", "Giám sát bảo mật"]
categories: ["Cyber Security", "Software Tool"]
---

![Chaos Mesh Kubernetes Vulnerability](/images/2025/chaos-mesh-vulnerability.png)

Chaos Mesh, một nền tảng kỹ thuật hỗn loạn (Chaos Engineering) mã nguồn mở phổ biến cho Kubernetes, đang phải đối mặt với các lỗ hổng an ninh nghiêm trọng. Các nhà nghiên cứu bảo mật của JFrog đã phát hiện ra bốn lỗ hổng nghiêm trọng (critical vulnerabilities), được đặt tên chung là "Chaotic Deputy", cho phép kẻ tấn công có quyền truy cập mạng nội bộ trong cụm Kubernetes thực thi lệnh tùy ý và leo thang đặc quyền, từ đó có thể chiếm quyền kiểm soát toàn bộ cụm. Ba trong số các lỗ hổng này có điểm CVSS 9.8 cực kỳ cao, nhấn mạnh tính cấp bách của việc hành động.

Người dùng Chaos Mesh được khuyến nghị **nâng cấp ngay lập tức lên phiên bản 2.7.3** để bảo vệ cụm Kubernetes của mình.

## Chaos Mesh là gì và hoạt động như thế nào?

Chaos Mesh là một nền tảng Cloud-Native Chaos Engineering được xây dựng trên Kubernetes Custom Resource Definitions (CRD). Mục tiêu của nó là giúp các kỹ sư và nhà phát triển kiểm tra khả năng phục hồi của hệ thống bằng cách mô phỏng các lỗi và sự cố trong môi trường sản xuất hoặc tiền sản xuất. Bằng cách giới thiệu các loại lỗi khác nhau như lỗi mạng, lỗi Pod, hoặc lỗi I/O, Chaos Mesh giúp xác định điểm yếu và cải thiện độ tin cậy của ứng dụng trên Kubernetes.

Kiến trúc Chaos Mesh bao gồm ba thành phần chính [N1]:

*   **Chaos Dashboard:** Giao diện người dùng (UI) để quản lý và cấu hình các thử nghiệm hỗn loạn.
*   **Chaos Controller Manager:** Thành phần cốt lõi chịu trách nhiệm lên lịch và quản lý các thử nghiệm hỗn loạn. Nó giám sát các Chaos CRD và điều phối việc thực thi lỗi.
*   **Chaos Daemon:** Chạy dưới dạng DaemonSet trên mỗi node Kubernetes. Thành phần này thực hiện việc "tiêm" lỗi thực tế vào các Pod hoặc node đích, ví dụ như sửa đổi cấu hình mạng, tập tin hệ thống hoặc kernel.

## Chi tiết về các lỗ hổng "Chaotic Deputy" (CVSS 9.8)

Các nhà nghiên cứu bảo mật của JFrog đã phát hiện và công bố một loạt lỗ hổng nghiêm trọng trong Chaos Mesh, được đặt tên chung là "Chaotic Deputy" [N2]. Các lỗ hổng này bao gồm:

*   **CVE-2025-59358**
*   **CVE-2025-59359 (CVSS 9.8)**
*   **CVE-2025-59360 (CVSS 9.8)**
*   **CVE-2025-59361 (CVSS 9.8)** [N2, N3]

**Tóm tắt vấn đề:** Các lỗ hổng này chủ yếu xoay quanh việc thiếu xác thực trên máy chủ gỡ lỗi GraphQL của Chaos Controller Manager, vốn được phơi bày trên toàn bộ cụm Kubernetes mà không yêu cầu bất kỳ hình thức xác thực nào. Điều này cho phép kẻ tấn công với quyền truy cập mạng nội bộ tối thiểu trong cụm thực hiện các hành động sau [N2, N3]:

*   **Thực thi lệnh hệ điều hành tùy ý (Arbitrary OS command injection):** Đặc biệt là trong quá trình "cleanIptables" của Chaos Controller Manager (liên quan đến CVE-2025-59361), kẻ tấn công có thể tiêm và thực thi các lệnh hệ điều hành.
*   **Leo thang đặc quyền (Privilege escalation):** Kết hợp với các lỗ hổng khác, điều này cho phép kẻ tấn công chiếm quyền kiểm soát toàn bộ cụm Kubernetes.
*   **Tấn công từ chối dịch vụ (Denial-of-Service - DoS):** Kẻ tấn công có thể gây gián đoạn hoặc vô hiệu hóa các dịch vụ.

Ngay cả các triển khai Chaos Mesh mặc định cũng dễ bị tấn công, biến đây thành một mối đe dọa đáng kể đối với bất kỳ môi trường Kubernetes nào sử dụng nền tảng này [N3].

## Ai bị ảnh hưởng?

*   Tất cả người dùng Chaos Mesh đang chạy các phiên bản trước **2.7.3**.
*   Các dịch vụ quản lý Kubernetes sử dụng Chaos Mesh, ví dụ như **Azure Chaos Studio**, cũng bị ảnh hưởng [N2].

## Khuyến nghị khẩn cấp: Nâng cấp lên phiên bản 2.7.3

Để bảo vệ cụm Kubernetes của bạn khỏi các lỗ hổng "Chaotic Deputy", việc nâng cấp lên Chaos Mesh phiên bản 2.7.3 là bắt buộc và cần được thực hiện khẩn cấp [N2].

Dưới đây là các bước nâng cấp bằng Helm:

1.  **Thêm hoặc cập nhật Helm Repository:**
    Đảm bảo bạn đã thêm kho lưu trữ (repository) của Chaos Mesh và cập nhật để có được phiên bản mới nhất.

    
```bash
    helm repo add chaos-mesh https://charts.chaos-mesh.org
    helm repo update
    ```


2.  **Cập nhật Custom Resource Definitions (CRDs):**
    Điều quan trọng là phải cập nhật các định nghĩa tài nguyên tùy chỉnh (CRD) để Chaos Mesh hoạt động chính xác với phiên bản mới.

    
```bash
    kubectl replace -f https://mirrors.chaos-mesh.org/v2.7.3/crd.yaml
    ```


    *Lưu ý: Hãy đảm bảo rằng CRD bạn sử dụng tương thích với phiên bản Kubernetes hiện tại của bạn.*

3.  **Nâng cấp Chaos Mesh qua Helm:**
    Thực hiện lệnh nâng cấp Helm, chỉ định rõ phiên bản 2.7.3.

    
```bash
    helm upgrade <release-name> chaos-mesh/chaos-mesh --namespace=<namespace> --version=2.7.3
    ```


    Thay thế `<release-name>` bằng tên release Helm của cài đặt Chaos Mesh của bạn và `<namespace>` bằng namespace nơi Chaos Mesh được triển khai.

4.  **Kiểm tra và cập nhật `values.yaml` (nếu có tùy chỉnh):**
    Nếu bạn đã tùy chỉnh tệp `values.yaml` cho triển khai Chaos Mesh của mình, hãy xem xét các thay đổi trong phiên bản 2.7.3 và cập nhật tệp của bạn cho phù hợp nhằm tránh bất kỳ sự cố cấu hình nào [N4].

## Kết luận

Các lỗ hổng "Chaotic Deputy" trong Chaos Mesh đại diện cho một rủi ro an ninh đáng kể đối với các cụm Kubernetes. Với khả năng thực thi lệnh tùy ý và leo thang đặc quyền, kẻ tấn công có thể dễ dàng chiếm đoạt quyền kiểm soát hoàn toàn môi trường của bạn. Hành động nhanh chóng và nâng cấp lên Chaos Mesh phiên bản 2.7.3 là biện pháp phòng ngừa hiệu quả nhất để giảm thiểu rủi ro này. Đừng chần chừ, hãy bảo vệ cụm Kubernetes của bạn ngay lập tức.

## Nguồn tham khảo
[N1] Chaos Mesh Overview. (n.d.). Retrieved from https://chaos-mesh.org/docs/
[N2] JFrog. (2025, September 16). Chaotic Deputy: Critical Vulnerabilities in Chaos Mesh Lead to Kubernetes Cluster Takeover. Retrieved from https://jfrog.com/blog/chaotic-deputy-critical-vulnerabilities-in-chaos-mesh-lead-to-kubernetes-cluster-takeover/
[N3] NVD. (2025, September 15). CVE-2025-59361 Detail. Retrieved from https://nvd.nist.gov/vuln/detail/CVE-2025-59361
[N4] Chaos Mesh. (n.d.). Upgrade from 2.1 to 2.2. Retrieved from https://chaos-mesh.org/docs/upgrade-from-2.1-to-2.2/