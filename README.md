# Địa Chỉ Đỏ Đồng Nai

Website tĩnh (HTML + Tailwind CDN + Font Awesome CDN), hoạt động như một "sổ hành trình": người dùng chọn **địa chỉ đỏ** (mỗi địa chỉ là một con tem) → chọn **câu chuyện / ảnh / video**.

## Cây thư mục

```text
dia-chi-do-dong-nai/
├── index.html                 Trang tổng: các card địa chỉ đỏ
├── map.html                   Bản đồ chung (Google My Maps)
├── firebase.json
├── README.md
│
└── nha-lao-tan-hiep/          ← mỗi địa chỉ đỏ là một thư mục
    ├── index.html             Giới thiệu chung + danh sách card câu chuyện
    ├── gallery.html           Thư viện ảnh
    ├── video.html             Danh sách video
    └── cau-chuyen/            Các câu chuyện (mỗi câu chuyện một file)
        ├── 01-nhung-nam-thang-lich-su.html
        ├── 02-pha-kham-tan-hiep-1956.html
        ├── 03-tuong-niem-nu-tu-chinh-tri-1974.html
        └── _mau-cau-chuyen.html   ← file mẫu để copy
```

Trong code, đoạn nào cần copy đều có dòng chú thích dạng `▼▼▼ … ▲▲▲`. Chỉ việc copy cả khối giữa hai dấu hiệu đó, dán ngay bên dưới rồi sửa chữ.

## Cách chạy

Nhấp đúp `index.html`, hoặc dùng VS Code + Live Server. Cần có mạng để tải Tailwind, font, ảnh và video.

## Thêm một câu chuyện mới

1. Vào `nha-lao-tan-hiep/cau-chuyen/`, copy `_mau-cau-chuyen.html`, đổi tên thành `04-ten-cau-chuyen.html`.
2. Mở file, sửa tiêu đề, ngày, ảnh, các đoạn văn, mốc thời gian, nguồn. Xóa dòng `<meta name="robots" content="noindex">`.
3. Mở `nha-lao-tan-hiep/index.html`, copy một khối **CARD CÂU CHUYỆN**, dán bên dưới, sửa `href="cau-chuyen/04-ten-cau-chuyen.html"`, ảnh, ngày, tiêu đề, mô tả.

## Thêm video

Mở `nha-lao-tan-hiep/video.html`, copy một khối **VIDEO YOUTUBE**, dán bên dưới, đổi mã video (11 ký tự sau `v=` trong link YouTube) ở link nhúng và link xem, rồi đổi tiêu đề, mô tả.
Video không nhúng được: copy khối **VIDEO NGUỒN KHÁC** và đổi link.

## Thêm ảnh

Mở `nha-lao-tan-hiep/gallery.html`, copy một khối **ẢNH**, dán bên dưới, đổi link ảnh (ở `href` và `src`), chú thích, nguồn. Ảnh được dẫn bằng link, không cần tải về.

## Thêm một địa chỉ đỏ mới

1. Copy cả thư mục `nha-lao-tan-hiep/`, đổi tên, ví dụ `chien-khu-d/`.
2. Trong thư mục mới, sửa `index.html` (tên, giới thiệu, thông tin), xóa bớt câu chuyện/video/ảnh cũ và thay bằng nội dung của địa chỉ mới. Chữ "Nhà lao Tân Hiệp" xuất hiện ở thanh tab, breadcrumb và hero của từng trang, cần đổi lại (dùng chức năng Tìm và Thay thế của VS Code trong thư mục mới).
3. Ở `index.html` ngoài cùng, copy khối **CARD ĐỊA CHỈ ĐỎ**, sửa `href` thành `chien-khu-d/index.html`, ảnh, tên, mô tả. (Hoặc thay một ô "SẮP RA MẮT" bằng card này.)
4. Ở `map.html`, copy khối **CARD ĐỊA CHỈ**.

Chân trang không có link riêng cho từng địa chỉ, nên không cần sửa footer.

## Bản đồ

Mở `map.html`, kéo xuống cuối file, thay giá trị:

```javascript
const MY_MAPS_URL = "THAY_URL_GOOGLE_MY_MAPS_CUA_TOI";
```

bằng URL nhúng của Google My Maps (Google My Maps → Chia sẻ công khai → ba chấm → *Nhúng vào trang web* → chép URL trong `src`). Khi chưa thay, trang hiện "Bản đồ đang được cập nhật".

Nút **Chỉ đường Google Maps** nằm ở trang giới thiệu của từng địa chỉ (`index.html` trong thư mục địa chỉ). Dán link Google Maps đã kiểm chứng vào `GOOGLE_MAPS_DIRECTIONS_URL` ở cuối file để bật nút.

## Đổi màu, chữ

Màu và phông chữ nằm ở khối `@theme` (đầu mỗi file HTML). Phông: Barlow Condensed (tiêu đề), Be Vietnam Pro (giao diện), Lora (bài viết).

## Đưa lên GitHub

```bash
git init
git add .
git commit -m "Địa Chỉ Đỏ Đồng Nai"
git branch -M main
git remote add origin https://github.com/<tai-khoan>/<ten-repo>.git
git push -u origin main
```

## Triển khai Firebase Hosting

```bash
npm install -g firebase-tools
firebase login
firebase use --add      # chọn dự án Firebase của bạn, giữ nguyên firebase.json
firebase deploy --only hosting
```

Lưu ý: `cau-chuyen/_mau-cau-chuyen.html` cũng sẽ được đưa lên khi deploy (đã gắn noindex). Nếu không muốn, hãy xóa file này trước khi deploy.
