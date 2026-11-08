# Tiếng Chuông Thiên Mụ

Trang chùa ảo nhiều người cùng vào: bến sông Hương trước chùa Thiên Mụ có con đò, chính điện, thỉnh chuông, thắp hương, xin xăm, thả hoa đăng gửi lời nguyện. Nhạc đàn tranh và đàn bầu theo hơi Nam Ai do trình duyệt tự chơi.

## Các file

| File | Dùng để |
|---|---|
| `index.html` | Toàn bộ trang (giao diện, cảnh vẽ, nhạc, 30 quẻ xăm) |
| `database.rules.json` | Luật bảo mật để dán vào Firebase |
| `README.md` | Hướng dẫn này |

Mở `index.html` ngay trên máy là chạy được **bản xem thử**: chỉ có một mình bạn, kèm vài "khách mẫu" để hình dung. Muốn mọi người thấy nhau thì làm thêm Phần 2.

---

## Phần 1. Đưa trang lên GitHub Pages (khoảng 10 phút, miễn phí)

1. Tạo tài khoản ở https://github.com (nếu chưa có).
2. Bấm **New repository**, đặt tên ví dụ `thien-mu`, chọn **Public**, rồi bấm **Create repository**.
3. Bấm **uploading an existing file** (hoặc **Add file → Upload files**), kéo thả `index.html` và `README.md` vào, rồi bấm **Commit changes**.
4. Vào **Settings → Pages**. Ở mục *Branch* chọn `main`, thư mục `/ (root)`, rồi bấm **Save**.
5. Khoảng 1–2 phút sau, trang chạy tại: `https://<tên-tài-khoản>.github.io/thien-mu/`

Muốn sửa chữ thì bấm vào `index.html` trên GitHub, chọn biểu tượng bút chì, sửa xong bấm **Commit changes**. Trang tự cập nhật sau khoảng 1 phút.

## Phần 2. Bật Firebase để nhiều người thấy nhau (khoảng 15 phút, miễn phí)

1. Vào https://console.firebase.google.com, bấm **Create a project** và đặt tên (Google Analytics không cần bật).
2. **Build → Authentication → Get started**, rồi:
   - bật **Anonymous** (khách vào không cần đăng nhập);
   - bật **Google** (chỉ để người quản trị xoá lời nguyện);
   - vào tab **Settings → Authorized domains**, bấm **Add domain** và thêm `<tên-tài-khoản>.github.io`.
3. **Build → Realtime Database → Create Database**, chọn vùng **Singapore (asia-southeast1)**, chọn **Start in locked mode**.
4. Vào tab **Rules** của Realtime Database:
   - xoá hết nội dung cũ rồi dán toàn bộ `database.rules.json`;
   - thay **cả 2 chỗ** `EMAIL_QUAN_TRI@gmail.com` bằng email Google của bạn;
   - bấm **Publish**.
5. Bấm **Project settings** (bánh răng), kéo xuống **Your apps**, chọn biểu tượng `</>` (Web) để đăng ký app. Firebase hiện ra một đoạn `firebaseConfig`.
6. Mở `index.html`, tìm khung **CẤU HÌNH** ở đầu phần script rồi sửa:
   ```js
   emailQuanTri: "email.cua.ban@gmail.com",
   firebase: {
     apiKey: "...",
     authDomain: "...",
     databaseURL: "https://...asia-southeast1.firebasedatabase.app",
     projectId: "...",
     appId: "..."
   }
   ```
   Mã `apiKey` của Firebase được phép để công khai. Thứ bảo vệ dữ liệu là bộ luật ở bước 4.
7. Tải `index.html` đã sửa lên GitHub (thay file cũ).

Từ đây, ai mở link cũng thấy nhau ở bến sông và trong chính điện. Ai thỉnh chuông thì mọi người cùng nghe, ai thả hoa đăng thì hoa trôi trên sông của mọi người.

**Quản trị:** mở bảng *Hoa đăng*, kéo xuống cuối và bấm **Quản trị**, rồi đăng nhập bằng đúng email đã khai. Khi đó mỗi lời nguyện có nút **Xóa** (bấm 2 lần để xác nhận).

## Tuỳ chỉnh nhanh (trong khung CẤU HÌNH)

- `tieuDe`, `moTa`: tiêu đề và câu giới thiệu ở màn đầu.
- `nhacNen`: muốn dùng bản thu ca Huế của riêng mình thì tải file mp3 lên cạnh `index.html` (ví dụ `nhac-hue.mp3`) và ghi tên file vào đây. **Chỉ dùng bản thu bạn có quyền sử dụng.**
- Quẻ xăm: sửa trong mảng `QUE` (30 quẻ, mỗi quẻ có bài thơ, lời bàn và 5 mục giải).

## Lưu ý

- Gói miễn phí của Firebase cho khoảng 100 người kết nối cùng lúc, dư dùng cho một cơ quan.
- Trang tự dọn các sự kiện chuông, hương cũ hơn 1 ngày. Lời nguyện được giữ lại cho đến khi quản trị xoá.
- Bộ luật đã chặn sửa hay xoá dữ liệu của người khác và giới hạn độ dài chữ. Tuy vậy, người cố ý vẫn có thể gửi liên tục. Nếu bị phá, hãy bật **App Check** trong Firebase.
- Đây là trang mô phỏng phi chính thức, không phải trang của chùa Thiên Mụ. Quẻ xăm do trang sáng tác theo tinh thần ca dao, để chiêm nghiệm.
- Kho mã trên GitHub để Public thì ai cũng xem được mã nguồn.
