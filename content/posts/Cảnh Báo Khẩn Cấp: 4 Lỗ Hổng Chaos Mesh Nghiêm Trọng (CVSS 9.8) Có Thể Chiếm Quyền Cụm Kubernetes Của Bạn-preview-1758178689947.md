---
title: "Cảnh Báo Khẩn Cấp: 4 Lỗ Hổng Chaos Mesh Nghiêm Trọng (CVSS 9.8) Có Thể Chiếm Quyền Cụm Kubernetes Của Bạn"
date: 2025-09-18T14:00:00.000+07:00
draft: false
tags: ["An ninh mạng", "Bảo mật hệ thống", "Lỗ hổng bảo mật", "Tấn công mạng", "Kubernetes", "Container", "DevOps", "Giám sát bảo mật", "API", "Quản lý rủi ro"]
categories: ["Cyber Security", "Software Tool"]
---

**Mở Đầu**

Trong thế giới phát triển phần mềm ngày càng phức tạp, việc đảm bảo tính ổn định và khả năng phục hồi của hệ thống là vô cùng quan trọng. Chaos Engineering đã nổi lên như một phương pháp mạnh mẽ để chủ động kiểm thử các điểm yếu trong hệ thống bằng cách cố ý gây ra sự cố. Chaos Mesh, một nền tảng Chaos Engineering mã nguồn mở dành cho Kubernetes, được Cloud Native Computing Foundation (CNCF) ươm tạo, là một công cụ phổ biến giúp các đội ngũ kiểm tra độ bền của môi trường Kubernetes.

Tuy nhiên, gần đây, một loạt bốn lỗ hổng bảo mật nghiêm trọng đã được phát hiện trong Chaos Mesh, được gán tên chung là **"Chaotic Deputy"** [3, 5]. Với điểm CVSS 9.8 (Critical), những lỗ hổng này có thể cho phép kẻ tấn công thực thi lệnh tùy ý và leo thang đặc quyền, dẫn đến việc chiếm quyền kiểm soát toàn bộ cụm Kubernetes [1, 2, 3, 5].

**Khuyến nghị khẩn cấp:** Người dùng Chaos Mesh được khuyến cáo **nâng cấp ngay lập tức lên phiên bản 2.7.3 hoặc cao hơn** để vá các lỗ hổng này [3, 5].

![Kiến trúc Chaos Mesh](/images/2025/chaos-mesh-architecture-2.0-8f9608a528cf0eaab88b05032cc8a1f8.png)
_Kiến trúc tổng quan của Chaos Mesh. Nguồn: chaos-mesh.org_

## Chaos Mesh và Tầm quan trọng của Chaos Engineering

Chaos Engineering là kỷ luật thử nghiệm hệ thống để tìm ra các điểm yếu bằng cách gây ra các sự cố có kiểm soát trong môi trường sản xuất hoặc thử nghiệm. Mục tiêu không phải là phá vỡ mọi thứ mà là hiểu rõ hơn về cách hệ thống hoạt động dưới áp lực và xây dựng khả năng phục hồi tốt hơn.

Chaos Mesh đơn giản hóa quá trình này trong Kubernetes. Nó cho phép người dùng mô phỏng nhiều loại lỗi khác nhau như tắt Pod, trễ mạng, lỗi DNS, hoặc lỗi hệ thống tập tin. Bằng cách quan sát cách ứng dụng phản ứng với những sự cố này, các nhà phát triển và vận hành có thể xác định và khắc phục các điểm yếu trước khi chúng gây ra sự cố nghiêm trọng trong thực tế.

## Phân tích chi tiết các Lỗ hổng nghiêm trọng (Chaotic Deputy)

Bộ lỗ hổng "Chaotic Deputy" bao gồm ba lỗ hổng thực thi lệnh từ xa (RCE) có điểm CVSS 9.8 và một lỗ hổng mức độ nghiêm trọng cao cho phép truy cập trái phép. Các lỗ hổng này ảnh hưởng đến các phiên bản Chaos Mesh trước 2.7.3 [3, 5].

**Bảng tổng hợp các CVEs quan trọng:**

| CVE ID | CVSS 3.1 | Attack Vector | Vulnerable Mutation | Mô tả / Tác động | Nguồn |
| :---------------- | :------- | :---------------------------------- | :-------------------- | :----------------------------------------------------------------------------------------------------------------- | :---------- |
| CVE-2025-59359 | 9.8 | In-cluster, unauthenticated GraphQL query | `cleanTcs` | Lỗi chèn lệnh OS qua tham số `cleanTcs` trong Chaos Controller Manager. Cho phép thực thi lệnh tùy ý. | [2, 4, 5] |
| CVE-2025-59360 | 9.8 | In-cluster, unauthenticated GraphQL query | `killProcesses` | Lỗi chèn lệnh OS qua tham số `killProcesses` trong Chaos Controller Manager. Cho phép thực thi lệnh tùy ý. | [2, 5] |
| CVE-2025-59361 | 9.8 | In-cluster, unauthenticated GraphQL query | `cleanIptables` | Lỗi chèn lệnh OS qua tham số `cleanIptables` trong Chaos Controller Manager. Cho phép thực thi lệnh tùy ý. | [2, 5, 6] |
| CVE-2025-59358 | 7.5 | In-cluster, unauthenticated access | GraphQL Debug endpoint | Cho phép truy cập trái phép vào endpoint GraphQL Debug, dẫn đến từ chối dịch vụ (DoS) và chèn lỗi trái phép. | [2, 5] |

### Cơ chế khai thác:

Các lỗ hổng RCE (CVE-2025-59359, CVE-2025-59360, CVE-2025-59361) đều xuất phát từ việc xử lý không an toàn dữ liệu đầu vào của người dùng trong các GraphQL mutations [1, 2, 5]. Cụ thể, Chaos Controller Manager đã ghép các chuỗi do người dùng cung cấp trực tiếp vào các lệnh shell mà không được làm sạch (sanitization) đúng cách. Kẻ tấn công, chỉ cần có quyền truy cập mạng nội bộ trong cụm Kubernetes (ví dụ: từ một Pod bị chiếm quyền), có thể gửi các truy vấn GraphQL độc hại để chèn và thực thi các lệnh OS tùy ý trên bất kỳ Pod nào mà Chaos Daemon có quyền truy cập [1, 2, 5].

### Ví dụ về tác động:

Một kẻ tấn công có thể sử dụng lỗ hổng này để:
*   Tắt các Pod quan trọng, gây gián đoạn dịch vụ.
*   Thực thi các lệnh độc hại để đánh cắp token tài khoản dịch vụ (service account tokens), từ đó leo thang đặc quyền trong cụm [1, 2, 3, 5].
*   Thay đổi cấu hình mạng (qua `cleanIptables`) hoặc tiêu diệt các tiến trình quan trọng (qua `killProcesses`) [2, 5].
*   Cuối cùng, chiếm quyền kiểm soát hoàn toàn cụm Kubernetes, truy cập dữ liệu nhạy cảm hoặc sử dụng cụm để thực hiện các cuộc tấn công khác [1, 2, 3, 5].

## Giải pháp và Khuyến nghị Khẩn cấp

Mức độ nghiêm trọng của các lỗ hổng này yêu cầu hành động ngay lập tức từ phía người dùng Chaos Mesh.

1.  **Nâng cấp Chaos Mesh lên phiên bản 2.7.3 hoặc cao hơn:** Đây là giải pháp triệt để và được khuyến nghị nhất. Phiên bản 2.7.3, phát hành vào ngày 21 tháng 8 năm 2025, đã vá tất cả các lỗ hổng "Chaotic Deputy" [3, 5].

    Để nâng cấp, bạn có thể tham khảo tài liệu chính thức của Chaos Mesh. Thông thường, quá trình này sẽ bao gồm việc cập nhật Helm chart hoặc YAML manifests:

    
```bash
    helm repo add chaos-mesh https://charts.chaos-mesh.org
    helm repo update
    helm upgrade chaos-mesh chaos-mesh/chaos-mesh --namespace=chaos-testing --version 2.7.3
    ```


    Hoặc cài đặt mới nếu chưa từng sử dụng:

    
```bash
    kubectl create ns chaos-testing
    helm install chaos-mesh chaos-mesh/chaos-mesh --namespace=chaos-testing --set controllerManager.leaderElection.leaderElect=true --set chaosDaemon.hostNetwork=true --version 2.7.3
    ```


2.  **Nếu không thể nâng cấp ngay lập tức:**
    *   **Hạn chế truy cập mạng vào API của Chaos Mesh:** Đảm bảo rằng Chaos Dashboard và Chaos Controller Manager không thể truy cập được từ bên ngoài cụm hoặc từ các Pod không đáng tin cậy. Sử dụng Network Policies để kiểm soát chặt chẽ luồng truy cập [5].
    *   **Tránh phơi bày nền tảng trong môi trường không an toàn:** Không triển khai Chaos Mesh trong môi trường mà các Pod có thể dễ dàng bị chiếm quyền hoặc không có kiểm soát truy cập nghiêm ngặt [5].

3.  **Thực hiện các biện pháp bảo mật tốt nhất cho Kubernetes:**
    *   Thường xuyên cập nhật các thành phần Kubernetes và các ứng dụng bên thứ ba.
    *   Áp dụng nguyên tắc đặc quyền tối thiểu (Least Privilege) cho tất cả các tài khoản dịch vụ (Service Accounts) và ứng dụng.
    *   Giám sát liên tục các hoạt động trong cụm để phát hiện hành vi bất thường.
    *   Sử dụng các công cụ quét lỗ hổng và kiểm tra cấu hình bảo mật.

## Kết luận

Các lỗ hổng "Chaotic Deputy" trong Chaos Mesh đặt ra một rủi ro nghiêm trọng đối với bất kỳ cụm Kubernetes nào sử dụng nền tảng này ở các phiên bản cũ hơn 2.7.3. Khả năng chiếm quyền cụm hoàn toàn thông qua việc thực thi lệnh tùy ý là một mối đe dọa không thể bỏ qua.

Việc ưu tiên nâng cấp lên Chaos Mesh phiên bản 2.7.3 là hành động cấp bách nhất để bảo vệ môi trường Kubernetes của bạn. Đồng thời, việc tuân thủ các thực hành bảo mật Kubernetes tốt nhất sẽ giúp giảm thiểu rủi ro từ các mối đe dọa hiện tại và tương lai. Đừng để Chaos Engineering của bạn biến thành một cuộc tấn công "chaos" thực sự!

## Nguồn tham khảo
[1] Infosecurity Magazine. (2025, September 17). *Critical CVEs in Chaos-Mesh Enable In-Cluster Code Execution*. [https://www.infosecurity-magazine.com/news/cves-chaos-mesh-cluster-code/](https://www.infosecurity-magazine.com/news/cves-chaos-mesh-cluster-code/)
[2] Gbhackers. (2025, September 17). *Chaos Mesh Critical Vulnerabilities Expose Kubernetes Clusters to Takeover*. [https://gbhackers.com/chaos-mesh-critical-vulnerabilities/](https://gbhackers.com/chaos-mesh-critical-vulnerabilities/)
[3] JFrog. (2025, September 16). *Chaotic Deputy: Critical Vulnerabilities in Chaos Mesh Lead to Kubernetes Cluster Takeover*. [https://jfrog.com/blog/chaotic-deputy-critical-vulnerabilities-in-chaos-mesh-lead-to-kubernetes-cluster-takeover/](https://jfrog.com/blog/chaotic-deputy-critical-vulnerabilities-in-chaos-mesh-lead-to-kubernetes-cluster-takeover/)
[4] CVE Details. (2025, September 15). *Vulnerability Details: CVE-2025-59359*. [https://www.cvedetails.com/cve/CVE-2025-59359/](https://www.cvedetails.com/cve/CVE-2025-59359/)
[5] The Hacker News. (2025, September 16). *Chaos Mesh Critical GraphQL Flaws Enable RCE and Full Cluster Takeover*. [https://thehackernews.com/2025/09/chaos-mesh-critical-graphql-flaws.html](https://thehackernews.com/2025/09/chaos-mesh-critical-graphql-flaws.html)
[6] Wiz. (2025, September 15). *CVE-2025-59361 Impact, Exploitability, and Mitigation Steps*. [https://www.wiz.io/vulnerability-database/cve/cve-2025-59361](https://www.wiz.io/vulnerability-database/cve/cve-2025-59361)