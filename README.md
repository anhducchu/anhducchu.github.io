# anhducchu.github.io

Personal academic website. Hugo + theme `barks` (lấy từ site của Nguyễn Vũ Thiên Trang),
bảng màu đen trắng.

## Sửa nội dung ở đâu

| Muốn sửa | File |
|---|---|
| Đoạn giới thiệu trang chủ | `content/_index.md` |
| Mục News | `content/news/_index.md` |
| Publications | `content/publications/_2026.md` (mỗi năm một file: `_2025.md`, `_2027.md`…) |
| Trang Background | `content/cv/_education.md`, `_research.md`, `_awards.md`, `_leadership.md`, `_skills.md` |
| Tên, email, link mạng xã hội, menu, **màu sắc** | `hugo.toml` |
| File CV PDF | `static/pdf/CV_ChuAnhDuc.pdf` |

Thứ tự các mục trên trang do `weight` trong front matter quyết định — số nhỏ hiện trước.

## Thêm ảnh chân dung

Bỏ ảnh vào `static/images/profile.jpg`, rồi mở dòng `image:` trong `content/_index.md`.
Không có ảnh thì phần chữ tự giãn full chiều rộng.

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

Sửa trong `hugo.toml`, mục `[params.colors]`:

```toml
background_color      = "#ffffff"   # nền sáng
text_color            = "#181818"
link_color            = "#000000"
name_blur_color       = "#c4c4c4"   # phần họ, xám nhạt trên header
dark_background_color = "#000000"   # nền tối
dark_text_color       = "#ededed"
dark_link_color       = "#ffffff"
dark_name_blur_color  = "#4a4a4a"
```
