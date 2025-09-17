---
title: "Hướng dẫn Định dạng Bài viết Markdown cho Hugo PaperMod"
date: 2024-07-30T10:30:00.000+07:00
draft: false
tags: ["Hugo", "PaperMod", "Markdown", "Blogging", "AI Formatting", "Static Site Generator", "Web Development"]
categories: ["Software Tool", "AI Data"]
---

![Cấu trúc file Markdown cho Hugo](/images/hugo_markdown_structure.webp)

Hugo là một trong những trình tạo trang web tĩnh phổ biến nhất, cho phép bạn xây dựng các trang web nhanh chóng và hiệu quả. Để tận dụng tối đa Hugo, đặc biệt với theme PaperMod, việc hiểu rõ cách định dạng bài viết Markdown là rất quan trọng. Bài viết này sẽ hướng dẫn bạn cách cấu trúc một file Markdown hoàn chỉnh, từ Front Matter đến các yếu tố nội dung.

## Cấu trúc Front Matter YAML

Mọi bài viết trên Hugo đều bắt đầu bằng một khối Front Matter ở định dạng YAML. Đây là nơi bạn định nghĩa các siêu dữ liệu quan trọng như tiêu đề, ngày xuất bản, thẻ (tags), và thể loại (categories).


```yaml
---
title: "Tiêu đề Bài viết Của Bạn"
date: 2024-07-30T10:30:00.000+07:00 # Định dạng RFC 3339
draft: false
tags: ["tag1", "tag2", "tag3"]
categories: ["Category Chính"]
---
```


*   `title`: Tiêu đề chính của bài viết, sẽ hiển thị trên trang.
*   `date`: Ngày và giờ xuất bản. Quan trọng để sắp xếp bài viết theo thời gian.
*   `draft`: Đặt `true` để giữ bài viết ở chế độ nháp, không hiển thị khi publish.
*   `tags`: Danh sách các từ khóa chi tiết liên quan đến nội dung.
*   `categories`: Danh sách các thể loại lớn mà bài viết thuộc về.

## Chèn Hình ảnh Minh họa

Hình ảnh giúp bài viết trở nên sinh động và dễ hiểu hơn. Bạn nên chèn một hình ảnh minh họa ngay sau phần mở đầu để thu hút người đọc.

Để chèn hình ảnh, sử dụng cú pháp Markdown tiêu chuẩn:


```markdown
![Mô tả ngắn gọn về hình ảnh](/images/ten_file_hinh_anh.webp)
```


Ví dụ:


```markdown
![Cấu trúc file Markdown cho Hugo](/images/hugo_markdown_structure.webp)
```


Đảm bảo rằng file ảnh được đặt trong thư mục `static/images` của dự án Hugo của bạn, hoặc đường dẫn tương ứng. Đường dẫn ảnh phải bắt đầu bằng `/images/NĂM_HIỆN_TẠI/tên_file_ảnh.ext` để tương thích với cấu trúc của Hugo. Ví dụ: `/images/2024/hugo_markdown_structure.webp`.

## Định dạng Nội dung Cơ bản

Hugo hỗ trợ đầy đủ cú pháp Markdown tiêu chuẩn. Dưới đây là một số yếu tố định dạng phổ biến:

### Tiêu đề

Sử dụng `#` để tạo tiêu đề, từ H1 đến H3.


```markdown
# Tiêu đề Cấp 1
## Tiêu đề Cấp 2
### Tiêu đề Cấp 3
```


### Danh sách

Sử dụng dấu gạch ngang (`-`) hoặc số để tạo danh sách.

*   Mục danh sách không thứ tự 1
*   Mục danh sách không thứ tự 2
    *   Mục con 1
    *   Mục con 2

1.  Mục danh sách có thứ tự 1
2.  Mục danh sách có thứ tự 2
    1.  Mục con có thứ tự 1
    2.  Mục con có thứ tự 2

### Khối Mã (Code Blocks)

Để hiển thị các đoạn mã, sử dụng ba dấu huyền (
```) và chỉ định ngôn ngữ lập trình để có cú pháp được tô sáng.

```
python
# Ví dụ mã Python
def hello_hugo():
    print("Hello from Hugo!")

hello_hugo()

```

```
bash
# Ví dụ mã Bash
hugo new posts/my-first-post.md
hugo server -D

```

### Bảng

Bạn có thể tạo bảng một cách dễ dàng trong Markdown:

| Header 1 | Header 2 | Header 3 |
| :------- | :------- | :------- |
| Row 1 Col 1 | Row 1 Col 2 | Row 1 Col 3 |
| Row 2 Col 1 | Row 2 Col 2 | Row 2 Col 3 |

### Biểu đồ Mermaid

Mặc dù Hugo PaperMod không hỗ trợ sẵn biểu đồ Mermaid, bạn có thể thêm hỗ trợ bằng cách tùy chỉnh theme hoặc sử dụng shortcode [3]. Điều này cho phép bạn tạo các biểu đồ và sơ đồ trực quan ngay trong Markdown.

```
mermaid
graph TD;
    A[Bắt đầu] --> B{Quyết định?};
    B --> C{Có};
    B --> D{Không};
    C --> E[Kết thúc];
    D --> E;

```

## Nguồn tham khảo

[Hugo Documentation](https://gohugo.io/documentation/)
[PaperMod Theme Documentation](https://adityatelange.github.io/hugo-PaperMod/)
[Markdown Guide](https://www.markdownguide.org/)
[3] Adding Mermaid support to PaperMod theme: [https://moebuta.org/posts/adding-mermaid-support-to-papermod-theme/](https://moebuta.org/posts/adding-mermaid-support-to-papermod-theme/)