# Cờ Thỉnh Kinh – Bản app & chơi online

Thư mục này là bản game có thể **cài lên điện thoại** (Android và iPhone) và **chơi online nhiều máy** qua Firebase.
Chưa cấu hình Firebase thì game vẫn chạy bình thường ở chế độ chơi trên một máy.

```
co-thinh-kinh-app/
├── index.html             trang game
├── firebase-config.js     ← dán cấu hình Firebase của bạn vào đây (Bước 4)
├── database.rules.json    ← luật bảo vệ dữ liệu, dán vào Firebase (Bước 3)
├── manifest.webmanifest   tên, biểu tượng khi cài lên điện thoại
├── sw.js                  cho phép mở game khi không có mạng
├── icons/                 biểu tượng app
└── vendor/                thư viện 3D và Firebase (đã kèm sẵn, không cần mạng để tải)
```

Tổng thời gian làm lần đầu: khoảng 20–30 phút. Chỉ cần một tài khoản Google, không tốn phí.

---

## Bước 1 – Tạo dự án Firebase

1. Vào **https://console.firebase.google.com**, đăng nhập Google.
2. Bấm **Create a project** (Tạo dự án), đặt tên, ví dụ `co-thinh-kinh`.
3. Màn hình hỏi Google Analytics: **tắt** đi (không cần), rồi **Create project**.

## Bước 2 – Bật đăng nhập ẩn danh

Người chơi không cần tạo tài khoản; mỗi máy được Firebase cấp một mã ẩn danh.

1. Menu trái: **Build → Authentication → Get started**.
2. Tab **Sign-in method** → chọn **Anonymous** → bật **Enable** → **Save**.

## Bước 3 – Tạo Realtime Database và dán luật

1. Menu trái: **Build → Realtime Database → Create Database**.
2. Chọn vị trí **Singapore (asia-southeast1)** cho gần Việt Nam → **Next**.
3. Chọn **Start in locked mode** → **Enable**.
4. Mở tab **Rules**, xoá hết nội dung đang có, mở file `database.rules.json` trong thư mục này, sao chép toàn bộ và dán vào → **Publish**.

Luật này đảm bảo: chỉ chủ phòng được ghi diễn biến ván cờ, mỗi người chỉ ngồi được ghế trống hoặc rời ghế của chính mình, và bài trên tay của ai chỉ người đó đọc được.

## Bước 4 – Lấy cấu hình và dán vào game

1. Bấm biểu tượng bánh răng cạnh **Project Overview** → **Project settings**.
2. Kéo xuống mục **Your apps** → bấm biểu tượng **`</>`** (Web).
3. Đặt tên app, ví dụ `Thinh Kinh Web` (không cần tick Firebase Hosting) → **Register app**.
4. Firebase hiện một đoạn `const firebaseConfig = { ... }`. Mở file `firebase-config.js` bằng Notepad/TextEdit và thay các giá trị cho khớp, ví dụ:

```js
window.CTK_FIREBASE_CONFIG = {
  apiKey: "AIzaSy...",
  authDomain: "co-thinh-kinh.firebaseapp.com",
  databaseURL: "https://co-thinh-kinh-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "co-thinh-kinh",
  appId: "1:1234567890:web:abcdef..."
};
```

- **databaseURL bắt buộc phải có.** Nếu đoạn Firebase đưa không có dòng này, lấy địa chỉ ở đầu tab **Data** của Realtime Database (dạng `https://...firebasedatabase.app`).
- `apiKey` của Firebase web không phải mật khẩu; dữ liệu được bảo vệ bằng luật ở Bước 3.

## Bước 5 – Đưa game lên mạng (miễn phí)

Game phải chạy từ một địa chỉ `https://` thì mới cài lên điện thoại và chơi online được. Chọn một cách:

**Cách nhanh nhất – Netlify Drop**
1. Vào **https://app.netlify.com/drop** (đăng ký miễn phí bằng email hoặc Google).
2. Kéo cả thư mục `co-thinh-kinh-app` thả vào trang.
3. Nhận link dạng `https://ten-ngau-nhien.netlify.app`. Có thể đổi tên ở **Site configuration → Change site name**.
4. Lần sau cập nhật: vào site → **Deploys** → kéo thả lại thư mục.

**Hoặc GitHub Pages** (nếu bạn dùng GitHub)
1. Tạo repository mới, tải toàn bộ file trong thư mục lên (giữ nguyên cấu trúc).
2. **Settings → Pages → Build and deployment → Deploy from a branch → main / (root) → Save**.
3. Sau 1–2 phút có link `https://ten-ban.github.io/ten-repo/`.

**Sau khi có link:** trong Firebase, vào **Authentication → Settings → Authorized domains → Add domain**, thêm tên miền vừa có (ví dụ `ten-ngau-nhien.netlify.app`).

## Bước 6 – Cài lên điện thoại

- **Android (Chrome):** mở link → bấm nút **Cài lên điện thoại** trên thanh menu của game, hoặc menu **⋮ → Cài đặt ứng dụng / Thêm vào màn hình chính**.
- **iPhone/iPad (Safari):** mở link → nút **Chia sẻ** → **Thêm vào MH chính**.

Biểu tượng ấn đỏ chữ 經 xuất hiện trên màn hình. Mở từ biểu tượng là game chạy toàn màn hình như app. Mở được cả khi không có mạng (trừ chế độ online).

---

## Cách chơi online

1. **Chủ phòng:** bấm **Ván mới → Chơi online**, nhập tên → **Tạo phòng mới**. Game hiện **mã phòng 5 ký tự** và link mời.
2. Gửi mã hoặc link cho bạn bè (Zalo, Messenger…). Nút **Chia sẻ** mở thẳng danh sách app chia sẻ của điện thoại.
3. **Người được mời:** mở link (hoặc vào **Chơi online**, nhập mã) → nhập tên → **Vào phòng** → bấm **Ngồi vào** ở một giới còn trống.
4. Chủ phòng chỉnh từng ghế: *Mở cho người chơi*, *Máy* hoặc *Bỏ trống*; chọn số quân cần về Kinh → **Bắt đầu ván**. Ghế còn trống lúc bắt đầu sẽ do máy cầm quân.
5. Trong ván, mỗi người chỉ điều khiển giới của mình; bài Phép trên tay chỉ mình thấy. Hiệu ứng, âm thanh và camera zoom hiện trên mọi máy.

**Khi mất kết nối**
- Người chơi mất mạng quá 15 giây đúng lượt của mình: máy đánh thay lượt đó; khi họ mở lại app sẽ tự vào lại đúng ghế.
- Chủ phòng là máy giữ luật. Chủ phòng mất mạng thì ván tạm dừng; chủ phòng mở lại app là ván tiếp tục từ chỗ cũ.
- Hết ván, chủ phòng bấm **Chơi lại cùng phòng** để về phòng chờ mà không phải mời lại.

**Sức chứa gói miễn phí:** Realtime Database gói Spark cho tối đa 100 kết nối cùng lúc, tức khoảng 25 phòng 4 người chơi đồng thời. Dữ liệu mỗi phòng chỉ vài chục KB. Muốn dọn phòng cũ: Realtime Database → tab **Data** → xoá nhánh `rooms` lúc không ai đang chơi.

---

## Cập nhật game về sau

Khi có bản mới, chỉ cần thay các file trong thư mục rồi đưa lên lại (Bước 5). Giữ nguyên `firebase-config.js` của bạn.
Mỗi bản mới có `VERSION` khác trong `sw.js` nên điện thoại tự nhận bản mới; người chơi chỉ cần đóng hẳn app rồi mở lại.

## Thử nhanh nhiều "máy" trên một máy tính (không cần Firebase)

Dành cho kiểm tra: mở trang với đuôi `?net=local` (ví dụ `https://ten-site.netlify.app/?net=local`) ở nhiều tab của cùng một trình duyệt. Mỗi tab đóng vai một máy, nói chuyện với nhau ngay trong trình duyệt.

## File APK cho Android

- File `CoThinhKinh.apk` nằm cùng thư mục với trang game. Tải trực tiếp tại `https://nogood84.github.io/co-thinh-kinh/CoThinhKinh.apk`, hoặc bấm **Cài lên điện thoại** trong game rồi chọn **Tải file APK cho Android**.
- Cài: mở file vừa tải, cho phép **Cài ứng dụng không rõ nguồn gốc** cho trình duyệt hoặc trình quản lý file khi máy hỏi, rồi bấm **Cài đặt**. Android 7 trở lên.
- App mở bản game trên GitHub Pages, nên mỗi lần cập nhật web là app có bản mới, không cần cài lại APK. Lần đầu mở mà không có mạng, app dùng bản có sẵn bên trong để chơi trên một máy.
- Khoá ký `cothinhkinh-release.p12` và mật khẩu được giữ riêng, không để trong thư mục này. Bản APK mới về sau phải ký bằng đúng khoá đó thì mới cài đè lên bản cũ được.

## Bước tiếp theo: CH Play và App Store

Khi bản web chạy ổn, có thể bọc thành app thật bằng **Capacitor**:
- **Google Play:** phí đăng ký 25 USD một lần; cần Android Studio để tạo file `.aab`.
- **App Store:** 99 USD mỗi năm; cần máy Mac có Xcode; Apple duyệt kỹ các app chỉ bọc trang web.
Phần này làm sau, dùng lại nguyên thư mục game hiện tại.
