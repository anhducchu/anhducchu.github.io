# anhducchu.github.io

Personal academic website. Hugo + theme `barks` (lấy từ site của Nguyễn Vũ Thiên Trang),
bảng màu đen trắng.

## Sửa nội dung ở đâu

| Muốn sửa | File |
|---|---|
| Đoạn giới thiệu trang chủ | `content/_index.md` |
| Mục News | `content/news/_index.md` |
| Publications | `content/publications/_2026.md` (mỗi năm một file: `_2025.md`, `_2027.md`…) |
| Trang About | `content/about/_education.md`, `_research.md`, `_academic.md`, `_awards.md`, `_leadership.md`, `_skills.md`, `_references.md` |
| Tên, email, link mạng xã hội, menu, **màu sắc** | `hugo.toml` |
| File CV PDF | `static/pdf/CV_ChuAnhDuc.pdf` (thay file là xong, giữ nguyên tên) |
| Ảnh chân dung | `static/images/profile.jpg` |
| Mô tả, từ khoá, tên biến thể (SEO) | `hugo.toml`, mục `[params.head]` và `[params.seo]` |

Thứ tự các mục trên trang do `weight` trong front matter quyết định — số nhỏ hiện trước.

## Thêm ảnh chân dung

Ảnh khai báo ở đầu file `content/_index.md`:

```yaml
---
title: "Home"
layout: landing_page
image: "/images/profile.jpg"
---
```

Chỉ cần bỏ file ảnh vào `static/images/profile.jpg` cho khớp đường dẫn đó là xong.
Muốn dùng tên file khác thì sửa dòng `image:` cho khớp.

Ảnh nên để dạng chân dung dọc, tỉ lệ khoảng 2:3.

Ảnh hiện tại đã nén sẵn về 880x1320, JPEG quality 84 (110 KB). Chỗ hiển thị chỉ rộng
221px nên không cần ảnh to hơn — đưa thẳng ảnh gốc vài MB lên sẽ làm trang tải chậm.
Khi thay ảnh mới thì nén lại tương tự:

```python
from PIL import Image
im = Image.open("anh-goc.jpg").convert("RGB")
im = im.resize((880, int(880*im.height/im.width)), Image.LANCZOS)
im.save("static/images/profile.jpg", "JPEG", quality=84, optimize=True, progressive=True)
```

Site có kiểm tra file tồn tại trước khi chèn: khi nào chưa push ảnh lên thì phần chữ
tự giãn full chiều rộng, không hiện icon ảnh vỡ. Nếu quên sửa `image:` mà cứ đặt tên
file là `profile.<ext>` thì site vẫn tự dò ra và dùng.

## Chạy thử ở máy

Cần Hugo **extended** (≥ 0.128):

```bash
hugo server
# mở http://localhost:1313
```

## Deploy

Push lên nhánh `main`, GitHub Actions (`.github/workflows/hugo.yml`) tự build và deploy
lên GitHub Pages. Trong repo Settings → Pages, chọn Source = **GitHub Actions**.

## Bảng màu

Đen trắng, sắc trung tính hơi ấm, **mặc định là nền sáng**. Tránh trắng tinh `#fff`
và đen tuyền `#000` vì tương phản 21:1 đọc lâu rất nhức mắt. Giá trị hiện tại đạt
12.9:1 (nền sáng) và 11.7:1 (nền tối) — thừa chuẩn WCAG AA 4.5:1 mà vẫn dịu.

Sửa ở `[params.colors]` trong `hugo.toml`. Đổi thì đo lại tương phản, và nhớ đổi kèm
màu công tắc trong `static/css/daynight.css`, `theme_color`, và dựng lại `og-card.jpg`.

Theme có sẵn hai param `background_gradient` và `dark_background_gradient` nếu sau này
muốn nền chuyển màu; hiện để trống nên nền phẳng. Nếu bật, phải đo tương phản ở **cả
các điểm dừng** của gradient chứ không chỉ với `background_color`.

## Chạy thử ở máy

Cần Hugo **extended** (>= 0.128):

```bash
hugo server
```
