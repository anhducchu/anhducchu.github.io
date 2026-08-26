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

**Mặc định là nền tối.** Tên biến trong `[params.colors]` vẫn theo theme gốc, dễ nhầm:

| Nhóm biến | Thực tế là |
|---|---|
| không có tiền tố (`background_color`, `link_color`…) | chế độ **sáng**, tông cyan — phải bấm công tắc mới thấy |
| có tiền tố `dark_` | **tím than**, đây mới là thứ hiện mặc định |

Nền là gradient, nên khi đổi màu chữ hoặc link phải đo tương phản ở **cả các điểm
dừng** của gradient chứ không chỉ với `background_color` — điểm sáng nhất mới là chỗ
chữ dễ chìm nhất. Ngưỡng WCAG AA là 4.5:1. Hiện tại: tối chữ 12.4:1 link 8.8:1,
sáng chữ 12.5:1 link 5.8:1.

Đổi bảng màu thì nhớ đổi kèm: màu công tắc trong `static/css/daynight.css`,
`theme_color` trong `hugo.toml`, và dựng lại `og-card.jpg`.

### Vì sao mặc định tối lại phức tạp hơn tưởng

`<body>` được render sẵn kèm `class="dark-theme"`, rồi có một script **nội tuyến ngay
sau thẻ `<body>`** gỡ lớp đó ra nếu người dùng đã chọn nền sáng. Script này phải nằm ở
đó, không được dời xuống `DOMContentLoaded` — nếu dời thì người chọn nền sáng sẽ thấy
trang nháy tối một nhịp rồi mới đổi.

Mọi lệnh gọi `localStorage` đều bọc `try/catch`: chế độ ẩn danh hoặc trình duyệt chặn
lưu trữ sẽ ném lỗi, không bọc thì hỏng luôn cái công tắc.

## Chạy thử ở máy

Cần Hugo **extended** (>= 0.128):

```bash
hugo server
```
