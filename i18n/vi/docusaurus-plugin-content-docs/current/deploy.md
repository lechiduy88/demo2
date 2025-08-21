# Bereitstellen

AI Short ist ein Open-Source-Projekt. Sie können den Namen und die Beschreibung der Website frei ändern.

- Um den Seitennamen zu ändern, bearbeiten Sie die Datei `docusaurus.config.js`.
- Um die Anweisungen zu ändern, gehen Sie in das Verzeichnis `docs`.
# Triển khai

AI Short là một dự án mã nguồn mở. Bạn có thể tự do thay đổi tên và mô tả của trang web.

- Để thay đổi **tên trang**, chỉnh sửa file `docusaurus.config.js`.  
- Để thay đổi **hướng dẫn**, chỉnh sửa trong thư mục `docs`.  
- Để thay đổi **các prompt**, bạn có thể chỉnh sửa trong file `src/data/prompt.json`.  
  Nếu chỉ cần thay đổi một ngôn ngữ, ví dụ tiếng Trung, bạn có thể chỉnh trực tiếp file `src/data/prompt_zh.json`.  
- Hiện tại, hệ thống người dùng đang kết nối với một backend chung. Nếu cần, bạn có thể xây dựng backend riêng của mình. Giao diện tương ứng nằm trong file `src/api.js`.

File `CodeUpdateHandler.py` là một script xử lý hàng loạt cho việc triển khai đa ngôn ngữ.  
Sau khi chỉnh sửa xong, chạy lệnh `python CodeUpdateHandler.py`. Script này sẽ tự động phân tách `prompt.json` thành nhiều ngôn ngữ theo quy tắc, đồng thời đồng bộ mã nguồn trang chính của từng ngôn ngữ và mã nguồn trang độc lập cho các prompt đã chọn.

---

## Hướng dẫn triển khai

### Yêu cầu hệ thống:

- [Node.js 18.0](https://nodejs.org/) hoặc mới hơn.  
- Hỗ trợ macOS, Windows (bao gồm WSL) và Linux.

### Triển khai cục bộ

Đảm bảo rằng bạn đã cài đặt [Node.js](https://nodejs.org/).

```shell
# Cài đặt
yarn

# Phát triển cục bộ
yarn start

# Build: Lệnh này sẽ tạo nội dung tĩnh trong thư mục `build`
yarn build

# Cập nhật giá trị `defaultLocale` trong file `docusaurus.config.js`, sau đó chạy build cho ngôn ngữ mong muốn.
yarn build --locale zh
yarn build --locale en
yarn build --locale ja
yarn build --locale ko
yarn build --locale es
yarn build --locale fr
yarn build --locale de
yarn build --locale it
yarn build --locale ru
yarn build --locale pt
yarn build --locale hi
yarn build --locale ar
yarn build --locale bn

# Triển khai đa ngôn ngữ
yarn build --locale zh && yarn build --locale en

```

### Triển khai với Vercel

Nhấn vào nút bên dưới để triển khai ChatGPT-Shortcut chỉ với một cú nhấp trên nền tảng Vercel:

[![Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Frockbenben%2FChatGPT-Shortcut%2Ftree%2Fmain)

**Lưu ý**: Phiên bản miễn phí của Vercel có thể gặp lỗi do thiếu dung lượng lưu trữ.  
Trong trường hợp này, bạn có thể giới hạn triển khai cho **một ngôn ngữ duy nhất**. Các bước thực hiện như sau:

1. Truy cập dự án Vercel vừa được triển khai và mở mục **Settings**.  
2. Trong phần **Build & Deployment**, tìm mục **Build Command** và nhấp vào **Override** ở bên phải.  
3. Thay đổi lệnh triển khai.  
   - Ví dụ: nếu bạn muốn triển khai phiên bản tiếng Trung, sử dụng `yarn build --locale zh`.  
   - Nếu muốn triển khai phiên bản tiếng Bồ Đào Nha, sử dụng `yarn build --locale pt`.

---

## Triển khai với Cloudflare Pages

Nhấn vào nút hoặc liên kết bên dưới để **fork dự án này**, sau đó làm theo hướng dẫn để triển khai trên Cloudflare Pages:

👉 [Fork dự án này](https://github.com/rockbenben/ChatGPT-Shortcut/fork)

### Các bước triển khai:

1. Đăng nhập vào [Cloudflare Pages](https://pages.cloudflare.com/) và chọn **“Create a project”**.  
2. Kết nối với repository vừa fork.  
3. Cấu hình lệnh build:  
   - **Build Command**: `yarn build --locale zh` (chọn ngôn ngữ tương ứng, ví dụ tiếng Bồ Đào Nha dùng `yarn build --locale pt`).  
   - **Output Directory**: `build`.  
4. Nhấn **Deploy** và chờ Cloudflare Pages hoàn tất quá trình build và triển khai.

Cloudflare Pages sẽ tự động chạy build và triển khai **mỗi khi bạn đẩy (push) code mới**.

---

### Triển khai với Docker

Nếu bạn quen thuộc với Docker, có thể nhanh chóng triển khai bằng lệnh sau:

```bash
# ghcr.io
docker run -d -p 3000:3000 --name chatgpt-shortcut ghcr.io/rockbenben/chatgpt-shortcut:latest

# docker hub
docker run -d -p 3000:3000 --name chatgpt-shortcut rockben/chatgpt-shortcut:latest
```

## Cập nhật đồng bộ

Nếu bạn triển khai dự án của riêng mình bằng một cú nhấp trên Vercel, có thể xảy ra tình trạng không nhận được cập nhật liên tục.  
Nguyên nhân là do Vercel mặc định tạo một dự án mới cho bạn thay vì fork dự án hiện tại, khiến việc nhận diện cập nhật không được chính xác.  

Khuyến nghị bạn nên thực hiện lại việc triển khai theo các bước sau:

1. Xóa repository trước đó.  
2. Sử dụng nút **“Fork”** ở góc trên bên phải để fork dự án hiện tại.  
3. Trên [trang Vercel “Neues Projekt”](https://vercel.com/new), chọn repository vừa fork trong phần **“Git-Repository importieren”** và tiến hành triển khai lại.

---

### Cập nhật tự động

> Nếu trong quá trình chạy **Upstream Sync** gặp lỗi, hãy thực hiện **đồng bộ fork thủ công** một lần.

Sau khi fork dự án, do hạn chế của GitHub, bạn cần vào tab **Actions** trong repository fork để bật workflows và kích hoạt hành động **Upstream Sync**.  
Sau khi kích hoạt, các bản cập nhật sẽ được đồng bộ tự động **mỗi ngày**.

![Cập nhật tự động](https://img.newzone.top/2023-05-19-11-57-59.png?imageMogr2/format/webp)

![Bật cập nhật tự động](https://img.newzone.top/2023-05-19-11-59-26.png?imageMogr2/format/webp)

---

### Cập nhật thủ công

Nếu bạn muốn cập nhật ngay lập tức bằng tay, có thể tham khảo [tài liệu GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) để biết cách đồng bộ repository fork với mã nguồn gốc (upstream).

---

👉 Hãy ủng hộ dự án này bằng cách **tặng sao (⭐)**, **theo dõi dự án**, hoặc **theo dõi tác giả** để luôn nhận được thông báo kịp thời về các tính năng mới.
