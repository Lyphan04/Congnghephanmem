# 💻 VQSTORE — Cửa Hàng Laptop & Phụ Kiện Công Nghệ

> **Đồ án môn học:** Công nghệ phần mềm (CNPM)  
> **Repository:** [https://github.com/Lyphan04/Congnghephanmem](https://github.com/Lyphan04/Congnghephanmem)

---

## 📖 Giới Thiệu Tổng Quan

**VQSTORE** là hệ thống website thương mại điện tử chuyên kinh doanh các dòng máy tính xách tay (Laptop Gaming, Laptop Văn Phòng, MacBook) cùng phụ kiện công nghệ (Bàn phím, Chuột, Tai nghe...). Hệ thống được thiết kế và xây dựng theo mô hình kiến trúc **MVC (Model - View - Controller)** kết hợp **Front Controller**, tối ưu hóa bảo mật, tốc độ và trải nghiệm người dùng.

---

## 🚀 Công Nghệ Sử Dụng

| Thành phần | Công nghệ |
| :--- | :--- |
| **Backend** | PHP (>= 7.4 / 8.x), OOP, MVC Architecture |
| **Cơ sở dữ liệu** | MySQL / MariaDB (Engine InnoDB, Charset `utf8mb4`) |
| **Thư viện CSDL** | Singleton PDO, Prepared Statements (chống SQL Injection) |
| **Frontend** | HTML5, CSS3, JavaScript (ES6+), FontAwesome |
| **Xác thực & Bảo mật** | Session Authentication, Bcrypt Password Hashing, Google OAuth 2.0 |
| **Gửi Email** | SMTP Gmail (Gửi mã xác thực đặt lại mật khẩu) |
| **Web Server** | Apache (hỗ trợ `mod_rewrite` qua `.htaccess`) |

---

## ✨ Tính Năng Nổi Bật

### 🛒 Dành Cho Khách Hàng (Client)
- **Trang chủ & Danh mục:** Hiển thị banner quảng cáo, sản phẩm mới, sản phẩm bán chạy, flash sale đếm ngược và phân loại theo danh mục (Gaming, Văn phòng, MacBook, Phụ kiện...).
- **Tìm kiếm & Bộ lọc:** Tìm kiếm từ khóa với gợi ý tức thì (Search Suggest), lọc theo khoảng giá, thương hiệu, sắp xếp giá/độ hot.
- **Chi tiết sản phẩm:** Xem thư viện ảnh, thông số kỹ thuật chi tiết (CPU, RAM, VGA, SSD...), đánh giá sao, bình luận và xem nhanh (Quick View).
- **Giỏ hàng & Đặt hàng:** Thêm/sửa/xóa sản phẩm, tự động tính tổng tiền, áp dụng phiếu giảm giá (Voucher), thanh toán COD / chuyển khoản.
- **Quản lý tài khoản:**
  - Đăng ký, đăng nhập tài khoản chuẩn và đăng nhập nhanh bằng **Google OAuth**.
  - Quên mật khẩu & cấp mã đặt lại qua Email SMTP.
  - Theo dõi lịch sử đơn hàng và tiến trình xử lý đơn hàng.
  - Danh sách sản phẩm yêu thích (Wishlist).
- **Liên hệ & Phản hồi:** Form gửi liên hệ, hỗ trợ trực tuyến tới bộ phận chăm sóc khách hàng.

### 🛡️ Dành Cho Quản Trị & Nhân Viên (Admin / Employee)
- **Bảng điều khiển (Dashboard):** Thống kê tổng doanh thu, số lượng đơn hàng, người dùng mới, biểu đồ tăng trưởng và cảnh báo hàng sắp hết kho.
- **Quản lý sản phẩm:** Thêm mới, cập nhật thông tin cấu hình (JSON specs), giá bán, giá flash sale, tải lên ảnh đại diện và ảnh thư viện.
- **Quản lý danh mục:** Quản lý nhóm hàng, danh mục cha-con, biểu tượng đại diện.
- **Quản lý đơn hàng:** Tiếp nhận đơn, cập nhật trạng thái (Chờ xác nhận, Đang giao, Đã giao, Đã hủy).
- **Quản lý người dùng & Phân quyền:** Phân cấp vai trò `super_admin`, `nhan_vien` (bán hàng, thủ kho), và `khach_hang`. Khóa/mở khóa tài khoản khi cần.
- **Quản lý khuyến mãi & Banner:** Tạo mã giảm giá (voucher), quản lý banner hero quảng cáo.
- **Quản lý liên hệ:** Tiếp nhận và trả lời thắc mắc của khách hàng.

---

## 📂 Cấu Trúc Thư Mục Dự Án

```plaintext
laptop_store-main/
├── assets/                 # Tài nguyên tĩnh (CSS, JS, Fonts, Images)
├── co_so_du_lieu/          # Script CSDL SQL (laptop_store.sql, migrations)
├── config/                 # File cấu hình hệ thống
│   ├── co_so_du_lieu.php   # Kết nối CSDL (PDO Singleton) & biến môi trường
│   ├── bi_mat.php          # Cấu hình tài khoản DB, SMTP, Google API
│   └── bi_mat.vi_du.php    # Mẫu cấu hình mẫu
├── controllers/            # Bộ điều khiển (MVC Controllers)
│   ├── DieuKhienTrangChu.php
│   ├── DieuKhienSanPham.php
│   ├── DieuKhienGioHang.php
│   ├── DieuKhienThanhToan.php
│   ├── DieuKhienDonHang.php
│   ├── DieuKhienTaiKhoan.php
│   ├── DieuKhienXacThuc.php
│   ├── DieuKhienQuanTri.php
│   └── ...
├── models/                 # Lớp tương tác CSDL (MVC Models)
│   ├── SanPham.php
│   ├── DanhMuc.php
│   ├── DonHang.php
│   ├── GioHang.php
│   ├── NguoiDung.php
│   └── ...
├── views/                  # Giao diện hiển thị (MVC Views)
├── thu_vien/               # Helper functions, xử lý session, tiện ích
├── tai_len/                # Thư mục lưu file upload (sản phẩm, avatar)
├── .htaccess               # Cấu hình URL Rewrite cho Apache
├── index.php               # Front Controller (Router trung tâm)
└── README.md               # Tài liệu dự án
```

---

## 🛠️ Hướng Dẫn Cài Đặt & Chạy Cục Bộ (Localhost)

### 1. Yêu cầu môi trường
- Cài đặt phần mềm máy chủ ảo: **XAMPP**, **WampServer**, hoặc **Laragon**.
- PHP phiên bản `>= 7.4` (khuyên dùng PHP 8.0 trở lên).
- MySQL / MariaDB phiên bản `>= 5.7` hoặc `>= 10.4`.
- Bật extension `pdo_mysql` và `curl` trong file `php.ini`.

### 2. Các bước triển khai

#### Bước 1: Tải mã nguồn về máy
Đặt thư mục dự án vào thư mục gốc của web server:
- Với XAMPP: `C:/xampp/htdocs/laptop_store`
- Với Laragon: `C:/laragon/www/laptop_store`

#### Bước 2: Import Cơ sở dữ liệu
1. Mở công cụ quản trị **phpMyAdmin** (thường là `http://localhost/phpmyadmin`).
2. Tạo một database mới tên: `laptop_store` (bảng mã: `utf8mb4_unicode_ci`).
3. Chọn tab **Import** và chọn file:  
   `co_so_du_lieu/laptop_store.sql`
4. Bấm **Import** để hoàn tất nạp bảng và dữ liệu mẫu.

#### Bước 3: Cấu hình thông tin kết nối
1. Kiểm tra file `config/bi_mat.php` (nếu chưa có, copy từ `config/bi_mat.vi_du.php`).
2. Cập nhật các thông số phù hợp với môi trường của bạn:
   ```php
   // ===== Database =====
   define('DB_HOST',    '127.0.0.1');
   define('DB_NAME',    'laptop_store');
   define('DB_USER',    'root');
   define('DB_PASS',    ''); // Để trống nếu dùng XAMPP mặc định
   define('DB_CHARSET', 'utf8mb4');

   // ===== SMTP (Gmail App Password) =====
   define('SMTP_USER', 'your_email@gmail.com');
   define('SMTP_PASS', 'your_app_password');
   define('MAIL_FROM', 'your_email@gmail.com');
   ```

3. Mở file `config/co_so_du_lieu.php` và kiểm tra hằng số `SITE_URL` trùng khớp với đường dẫn dự án của bạn (mặc định: `http://localhost/laptop_store`).

#### Bước 4: Khởi chạy và trải nghiệm
- **Trang chủ Khách hàng:** `http://localhost/laptop_store`
- **Trang Quản trị Admin:** `http://localhost/laptop_store/admin`

---

## 🐧 Hướng Dẫn Triển Khai & Chạy Trên Ubuntu (Linux)

Dự án hoàn toàn tương thích và chạy tối ưu trên môi trường **Ubuntu (LAMP Stack)**:

### Bước 1: Cài đặt LAMP Stack trên Ubuntu
Mở Terminal trên Ubuntu và chạy các lệnh:
```bash
sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql php-curl php-mbstring -y
```

### Bước 2: Bật module URL Rewrite cho Apache
```bash
sudo a2enmod rewrite
```
Mở file cấu hình Apache:
```bash
sudo nano /etc/apache2/apache2.conf
```
Tìm đến khối `<Directory /var/www/>` và đổi `AllowOverride None` thành `AllowOverride All`:
```apache
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```
Lưu lại (`Ctrl + O`, `Enter`, `Ctrl + X`) rồi khởi động lại Apache:
```bash
sudo systemctl restart apache2
```

### Bước 3: Đưa mã nguồn vào thư mục web
```bash
# Di chuyển vào thư mục web
cd /var/www/html

# Clone dự án từ GitHub
sudo git clone https://github.com/Lyphan04/Congnghephanmem.git laptop_store

# Phân quyền cho Apache và thư mục upload ảnh
sudo chown -R www-data:www-data /var/www/html/laptop_store
sudo chmod -R 775 /var/www/html/laptop_store/tai_len
```

### Bước 4: Tạo CSDL & Import dữ liệu
```bash
# Đăng nhập MySQL
sudo mysql -u root

# Trong MySQL console, tạo CSDL:
CREATE DATABASE laptop_store CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
EXIT;

# Import file SQL mẫu vào CSDL:
sudo mysql -u root laptop_store < /var/www/html/laptop_store/co_so_du_lieu/laptop_store.sql
```

### Bước 5: Cấu hình bí mật và trải nghiệm
Chỉnh sửa file cấu hình kết nối DB (nếu MySQL có đặt mật khẩu):
```bash
sudo nano /var/www/html/laptop_store/config/bi_mat.php
```
Mở trình duyệt trên Ubuntu và truy cập:
- `http://localhost/laptop_store` (hoặc `http://<IP_Ubuntu>/laptop_store` nếu truy cập từ máy khác).

## 🔑 Tài Khoản Trải Nghiệm Mẫu

Sau khi import file `co_so_du_lieu/laptop_store.sql`, bạn có thể đăng nhập bằng các tài khoản mẫu sau:

| Vai trò | Email đăng nhập | Mật khẩu mặc định | Ghi chú |
| :--- | :--- | :--- | :--- |
| **Quản trị viên (Super Admin)** | `admin@vqstore.vn` | `Admin@123` | Toàn quyền quản trị hệ thống |
| **Nhân viên bán hàng** | `sales@vqstore.vn` | `Employee@123` | Xử lý đơn hàng, kho |
| **Khách hàng mẫu** | `user@vqstore.vn` | `User@123` | Mua sắm, đánh giá, wishlist |

---

## 📄 Tài Liệu Báo Cáo Kèm Theo
- [CHUONG_2_BAO_CAO.md](CHUONG_2_BAO_CAO.md): Chi tiết báo cáo phân tích chương 2.
- [CHUONG_2_KHAO_SAT_HIEN_TRANG.md](CHUONG_2_KHAO_SAT_HIEN_TRANG.md): Khảo sát hiện trạng đề tài.
- [HOI_DAP_CODE.md](HOI_DAP_CODE.md): Bộ câu hỏi và đáp code phục vụ bảo vệ đồ án.

---

## 👥 Tác Giả & Đóng Góp
- **Dự án:** Đồ án Công nghệ phần mềm
- **GitHub:** [@Lyphan04](https://github.com/Lyphan04)
