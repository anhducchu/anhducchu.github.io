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
| File CV PDF | `static/pdf/CV_ChuAnhDuc.pdf` (thay file là xong, giữ nguyên tên) |
| Ảnh chân dung | `static/images/profile.jpg` |

Thứ tự các mục trên trang do `weight` trong front matter quyết định — số nhỏ hiện trước.

## Thêm ảnh chân dung

Bỏ file ảnh vào `static/images/` và đặt tên là `profile` — `profile.jpg`, `profile.png`,
`profile.webp` đều được. Site tự nhận, **không cần sửa config gì thêm**.

Chưa có ảnh thì phần chữ tự giãn full chiều rộng, không bị vỡ layout hay hiện icon ảnh lỗi.

Ảnh nên để dạng chân dung dọc, tỉ lệ khoảng 2:3 (ví dụ 440×660 px). Muốn dùng file tên
khác thì khai báo trong `content/_index.md`: `image: "/images/ten-file.jpg"`.

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

## Lưu ý kỹ thuật

`disablePathToLower = true` trong `hugo.toml` là bắt buộc, đừng xoá. Mặc định Hugo
đổi URL trong menu thành chữ thường, biến `/pdf/CV_ChuAnhDuc.pdf` thành
`/pdf/cv_chuanhduc.pdf` — GitHub Pages phân biệt hoa thường nên link CV sẽ 404.
Toàn bộ file trong `content/` đang đặt tên chữ thường nên cờ này không ảnh hưởng
URL của các trang.
