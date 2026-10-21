# Báo cáo kiểm thử VQStore

| Thông tin | Giá trị |
| --- | --- |
| Dự án | `Congnghephanmem-main` |
| Hạng mục | QA Testing của Thảo |
| Ngày thực hiện | 21/10/2026 |
| Môi trường | Localhost, Windows, XAMPP, PHP 8.0.30, MySQL, Chromium |
| Trạng thái | Đã kiểm thử và sửa 6 nhóm lỗi; còn 5 nhóm lỗi cần xử lý |

## 1. Kết luận

Đã kiểm tra giao diện desktop/mobile, các thao tác sử dụng chính, xử lý 404 và một số API của VQStore. Các chỉnh sửa đã giúp trang tải đúng tài nguyên, mở được chi tiết sản phẩm, khôi phục model được API sử dụng và thao tác bộ lọc trên mobile.

Kết quả chưa đủ để kết luận toàn bộ hệ thống đạt yêu cầu. Các lỗi cần ưu tiên tiếp theo là trang Liên hệ, trang Yêu thích và xác minh số điện thoại khi tra cứu đơn hàng. Báo cáo phân biệt kết quả hiển thị, kết quả thao tác và các chức năng chưa kiểm thử đầu cuối.

## 2. Phạm vi và phương pháp

- Kiểm thử giao diện có hỗ trợ tự động trên trình duyệt; đối chiếu DOM và ảnh chụp các màn hình chính.
- Kiểm tra lỗi PHP hiển thị, ảnh không tải, tràn ngang toàn trang và phần tử nội dung vượt viewport.
- Thực hiện các thao tác sản phẩm, bộ lọc, giỏ hàng, form thanh toán, đơn hàng và điều hướng quản trị.
- Gửi yêu cầu HTTP GET để kiểm tra mã phản hồi, chuyển hướng và JSON của API.
- Chạy `php -l` trên mã nguồn PHP để kiểm tra cú pháp.

### 2.1. Môi trường

| Thiết lập | Giá trị |
| --- | --- |
| URL kiểm thử | `http://localhost/congnghephanmem-main/` |
| Desktop | 1440 × 900 px |
| Tablet | 768 × 844 px |
| Mobile | 390 × 844 px và 360 × 844 px |
| Dữ liệu riêng cho QA | 1 tài khoản và 2 đơn hàng tạm, gồm `pending` và `completed` |

Các kích thước mobile/tablet được mô phỏng trong Chromium. Chưa kiểm thử trên thiết bị Android/iPhone thật hoặc nhiều trình duyệt. Các bản ghi QA được tạo riêng để kiểm tra các màn hình cần đăng nhập và đã được dọn sau phiên thử.

### 2.2. Tổng hợp kết quả

| Nhóm kiểm tra | Khối lượng | Kết quả |
| --- | --- | --- |
| Hiển thị và responsive | 32 màn hình × 4 kích thước = 128 lượt | 116 lượt đạt theo tiêu chí kiểm tra; 12 lượt còn lỗi |
| Thao tác thực tế | 23 ca | 22 đạt; 1 không đạt |
| HTTP và API | 31 yêu cầu GET | Kết quả chi tiết tại mục 5 |
| Cú pháp PHP | 68 file | 68 đạt; 0 lỗi cú pháp |

12 lượt hiển thị còn lỗi gồm Liên hệ và Yêu thích ở cả 4 kích thước, cùng ảnh đại diện mặc định trên Hồ sơ ở cả 4 kích thước. Một lỗi có thể lặp lại ở nhiều kích thước; số lượt lỗi không phải số lỗi độc lập.

## 3. Ma trận kiểm tra hiển thị sau sửa

**Tiêu chí:** trang tải được, không có lỗi PHP hiển thị, không có ảnh lỗi và không phát hiện tràn ngang ngoài viewport theo phép đo DOM. Bảng có vùng cuộn ngang riêng được chấp nhận. Kết quả “Đạt” trong bảng này chỉ phản ánh tiêu chí hiển thị; không xác nhận toàn bộ nghiệp vụ của màn hình.

| Màn hình | 1440 px | 768 px | 390 px | 360 px |
| --- | --- | --- | --- | --- |
| Trang chủ | Đạt | Đạt | Đạt | Đạt |
| Danh sách laptop | Đạt | Đạt | Đạt | Đạt |
| Danh sách phụ kiện | Đạt | Đạt | Đạt | Đạt |
| Chi tiết sản phẩm | Đạt | Đạt | Đạt | Đạt |
| Giỏ hàng có sản phẩm | Đạt | Đạt | Đạt | Đạt |
| Form thanh toán | Đạt | Đạt | Đạt | Đạt |
| Hồ sơ cá nhân | Lỗi ảnh | Lỗi ảnh | Lỗi ảnh | Lỗi ảnh |
| Danh sách đơn hàng | Đạt | Đạt | Đạt | Đạt |
| Chi tiết đơn hàng | Đạt | Đạt | Đạt | Đạt |
| Xác nhận đặt hàng thành công | Đạt | Đạt | Đạt | Đạt |
| Lịch sử mua hàng | Đạt | Đạt | Đạt | Đạt |
| Thông báo | Đạt | Đạt | Đạt | Đạt |
| Danh sách yêu thích | Lỗi view | Lỗi view | Lỗi view | Lỗi view |
| Khuyến mãi | Đạt | Đạt | Đạt | Đạt |
| Liên hệ | Lỗi view | Lỗi view | Lỗi view | Lỗi view |
| Form tra cứu đơn hàng | Đạt | Đạt | Đạt | Đạt |
| 404 cho đường dẫn lạ | Đạt | Đạt | Đạt | Đạt |
| 404 cho action không tồn tại | Đạt | Đạt | Đạt | Đạt |
| Admin Dashboard | Đạt | Đạt | Đạt | Đạt |
| Admin doanh thu | Đạt | Đạt | Đạt | Đạt |
| Admin sản phẩm | Đạt | Đạt | Đạt | Đạt |
| Admin đơn hàng | Đạt | Đạt | Đạt | Đạt |
| Admin khách hàng | Đạt | Đạt | Đạt | Đạt |
| Admin nhân viên | Đạt | Đạt | Đạt | Đạt |
| Admin voucher | Đạt | Đạt | Đạt | Đạt |
| Admin đánh giá | Đạt | Đạt | Đạt | Đạt |
| Admin liên hệ | Đạt | Đạt | Đạt | Đạt |
| Admin gửi thư | Đạt | Đạt | Đạt | Đạt |
| Đăng nhập khách hàng | Đạt | Đạt | Đạt | Đạt |
| Đăng ký | Đạt | Đạt | Đạt | Đạt |
| Quên mật khẩu | Đạt | Đạt | Đạt | Đạt |
| Đăng nhập admin | Đạt | Đạt | Đạt | Đạt |

## 4. Các ca thao tác đã thực hiện

Sản phẩm dùng trong ca giỏ hàng là ASUS ROG Strix G15, đơn giá tại thời điểm kiểm thử là **27.990.000đ**. Các ca đơn hàng dùng dữ liệu riêng của tài khoản QA.

| Mã | Thao tác / dữ liệu | Kết quả thực tế | Đánh giá |
| --- | --- | --- | --- |
| F01 | Đăng nhập tài khoản QA | Mở được hồ sơ của tài khoản QA và hiển thị các đơn thuộc tài khoản | Đạt |
| F02 | Chọn thumbnail `View 3` trong gallery | Ảnh chính đổi từ ảnh `.1.webp` sang `.2.webp` | Đạt |
| F03 | Thêm sản phẩm từ trang chi tiết, mở giỏ | Giỏ có 1 sản phẩm, đơn giá 27.990.000đ | Đạt |
| F04 | Tăng số lượng trong giỏ từ 1 lên 2 | Tổng đổi thành 55.980.000đ | Đạt |
| F05 | Giảm số lượng từ 2 về 1 | Tổng trở lại 27.990.000đ | Đạt |
| F06 | Áp dụng mã `QA-KHONG-TON-TAI` | Báo “Mã voucher không tồn tại”, tổng không đổi | Đạt |
| F07 | Bỏ trống địa chỉ rồi bấm đặt hàng | Trình duyệt chặn do thiếu trường bắt buộc; vẫn ở checkout | Đạt |
| F08 | Mở bộ lọc sản phẩm trên mobile | Hiển thị lựa chọn dòng máy và mức giá | Đạt |
| F09 | Chọn dòng MacBook | Hiển thị 4 sản phẩm, đều là MacBook | Đạt |
| F10 | Chọn sắp xếp giá tăng dần sau khi lọc | Thứ tự 25.990.000 → 29.990.000 → 38.990.000 → 54.990.000đ | Đạt |
| F11 | Chuyển danh sách laptop sang trang 2 | Hiển thị 4 sản phẩm còn lại | Đạt |
| F12 | Tìm kiếm `MacBook` | Hiển thị 4 kết quả MacBook | Đạt |
| F13 | Bấm Menu trên mobile | Drawer điều hướng mở | Đạt |
| F14 | Bấm xem nhanh trên thẻ sản phẩm | Modal hiển thị MacBook Air M2, giá và liên kết chi tiết | Đạt |
| F15 | Mở danh sách đơn của tài khoản QA | Hiển thị 2 đơn ở trạng thái Chờ xác nhận và Hoàn thành | Đạt |
| F16 | Mở chi tiết một đơn QA | Hiển thị đúng mã, sản phẩm và thông tin của đơn | Đạt |
| F17 | Mở lịch sử mua hàng | Hiển thị 1 sản phẩm của đơn hoàn thành, tổng 27.990.000đ | Đạt |
| F18 | Lọc trạng thái Hoàn thành | Chỉ còn 1 đơn QA hoàn thành | Đạt |
| F19 | Mở trang success với một đơn QA có sẵn | Trang xác nhận thành công tải được | Đạt về hiển thị |
| F20 | Chọn “7 ngày qua” trong báo cáo doanh thu | Tiêu đề biểu đồ đổi theo khoảng thời gian | Đạt |
| F21 | Mở menu quản trị ở mobile | Sidebar quản trị mở và có các mục điều hướng | Đạt |
| F22 | Đăng xuất, tra cứu chỉ với mã đơn QA | Xem được tên, điện thoại và địa chỉ mà không cần xác minh SĐT | Không đạt — B03 |
| F23 | Bấm “Về trang chủ” tại trang 404 | Trở về trang chủ và hiển thị danh mục sản phẩm | Đạt |

**Giới hạn của F19:** đơn được tạo trực tiếp trong CSDL để kiểm tra view. Kết quả này không xác nhận luồng submit tạo đơn, transaction, trừ kho, gửi email hoặc thanh toán đầu cuối đã hoạt động đúng.

## 5. Kết quả HTTP và API

| Trường hợp | Kết quả sau sửa |
| --- | --- |
| Trang chủ, danh sách laptop/phụ kiện, chi tiết, giỏ, khuyến mãi | HTTP 200; không phát hiện lỗi PHP trong nội dung trả về |
| Chưa đăng nhập vào checkout, order, account/history, wishlist | Chuyển về `/auth/login` trong đúng thư mục dự án |
| Slug sản phẩm không tồn tại | Chuyển tới trang 404; phản hồi cuối HTTP 404 |
| URL gốc lạ | HTTP 404 và trang lỗi thân thiện |
| Action lạ của cart, account, admin | HTTP 404; không còn lỗi gọi phương thức không tồn tại |
| `/api/qa-khong-ton-tai` | HTTP 404; JSON hợp lệ và đúng Content-Type JSON |
| `/api/search?q=MacBook` | HTTP 200; JSON hợp lệ; 4 sản phẩm |
| Tìm kiếm rỗng hoặc từ khóa không khớp | HTTP 200; JSON hợp lệ; mảng sản phẩm rỗng |
| `/api/cart` trong phiên khách rỗng | HTTP 200; JSON hợp lệ |
| Tra cứu mã đơn không tồn tại | Trang tải được và phản hồi không tìm thấy đơn |
| `/contact` | Còn Warning/Fatal error do thiếu view, dù HTTP trả 200 |
| 9 liên kết nội dung ở chân trang | Đều trả 404; chi tiết B04 |

HTTP 200 không tự động được xem là đạt. Kết quả cũng được kiểm tra về nội dung lỗi và khả năng sử dụng. Mẫu thời gian phản hồi trên localhost không được dùng để kết luận hiệu năng hoặc khả năng chịu tải.

## 6. Các lỗi đã sửa

| Mã | Vấn đề trước sửa | Xử lý | Kết quả xác minh |
| --- | --- | --- | --- |
| S01 | SITE_URL trỏ `/laptop_store`, RewriteBase/ErrorDocument trỏ `/laptop_store-main`; trang thiếu CSS/ảnh và có 71 liên kết sai thư mục | Đồng bộ đường dẫn cài đặt với `/congnghephanmem-main` | Trang chủ tải được CSS/ảnh; không còn liên kết `/laptop_store` tại lần kiểm tra |
| S02 | Thiếu `views/san_pham/chi_tiet.php`, trong khi view đang nằm ở thư mục gốc | Sao chép nguyên view có sẵn vào đường dẫn controller yêu cầu | Chi tiết sản phẩm, gallery và thêm giỏ hoạt động |
| S03 | Thiếu `models/YeuThich.php`; class đang nằm trong thư mục views | Sao chép nguyên model vào đúng đường dẫn được require | API tìm kiếm và giỏ hàng trả JSON hợp lệ trở lại |
| S04 | Bộ lọc bị ẩn dưới 900 px nhưng không có nút mở | Thêm nút, thuộc tính ARIA, CSS và JavaScript đóng/mở | Mở được bộ lọc mobile; chọn MacBook trả 4 kết quả |
| S05 | Tên chứa mã CPU/GPU dài tràn khỏi thẻ sản phẩm | Thêm `overflow-wrap: anywhere` vào liên kết tên sản phẩm | Không phát hiện phần tử nội dung tràn ngang trong các lượt hồi quy sau sửa |
| S06 | Action không tồn tại gây lỗi PHP; action admin lạ về Dashboard | Kiểm tra khả năng gọi method trước khi điều phối; trả 404 khi không hợp lệ | Các URL action lạ đã thử trả 404; API lạ trả JSON 404 |

### 6.1. Danh sách thay đổi mã nguồn

Có **6 file sửa và 2 file thêm**. Số dòng dưới đây được đối chiếu với phiên bản sau QA ngày 21/10/2026; có thể thay đổi khi nhóm sửa tiếp.

| File | Loại | Vị trí | Nội dung / phạm vi ảnh hưởng |
| --- | --- | --- | --- |
| `config/co_so_du_lieu.php` | Sửa | Dòng 9 | Đổi SITE_URL; ảnh hưởng các URL dẫn xuất, gồm assets và OAuth redirect |
| `.htaccess` | Sửa | Dòng 4, 43 | RewriteBase và ErrorDocument cho thư mục cài đặt |
| `index.php` | Sửa | Dòng 24–32 và các chỗ gọi action; điều kiện API dòng 127 | Thêm helper gọi action, áp dụng cho cart, checkout, order, account, auth, admin, wishlist; điều chỉnh kiểm tra method API |
| `assets/css/style.css` | Sửa | Dòng 901 | Ngắt dòng tên sản phẩm; ảnh hưởng các thẻ dùng CSS chung |
| `assets/css/product.css` | Sửa | Dòng 494, 512–525 | CSS nút mở bộ lọc khi viewport rộng tối đa 900 px |
| `views/san_pham/danh_sach.php` | Sửa | Dòng 403–407, 427, 546–558 | Nút mở bộ lọc, id panel, JavaScript đóng/mở và giữ trạng thái khi đã chọn |
| `views/san_pham/chi_tiet.php` | Thêm | Toàn file 805 dòng | Sao chép nguyên từ `chi_tiet.php` ở gốc |
| `models/YeuThich.php` | Thêm | Toàn file 71 dòng | Sao chép nguyên từ `views/taikhoan/YeuThich.php` |

### 6.2. Các điểm cần phối hợp khi ghép code

- `SITE_URL`, `RewriteBase` và `ErrorDocument` phụ thuộc tên thư mục của từng máy; thống nhất cấu hình trước khi ghép.
- `index.php` và CSS dùng chung cần được đối chiếu cùng người phụ trách các module liên quan. Action admin không tồn tại hiện trả 404, thay cho chuyển về Dashboard.
- Helper mới dùng `str_starts_with`, yêu cầu PHP 8 trở lên. Helper kiểm tra method có thể gọi; chưa phải danh sách trắng action nghiệp vụ.
- Thay đổi CSS bộ lọc và view danh sách phải được ghép cùng nhau.
- Theo bản phân công, trang chi tiết và model yêu thích thuộc hạng mục Quyên. Hai file thêm mới giống nguyên nội dung nguồn tại thời điểm sao chép; nhóm cần thống nhất file chính để sửa tiếp.
- Controller hiện dùng `views/san_pham/chi_tiet.php` và `models/YeuThich.php`. Sửa riêng các bản nguồn cũ ở vị trí khác sẽ chưa cập nhật các đường dẫn đang được dùng. Không include đồng thời hai file cùng khai báo class `YeuThich`.

## 7. Lỗi còn tồn tại

Các lỗi sau được ghi nhận trong phiên QA và chưa được sửa trong phạm vi báo cáo này. Mức độ dưới đây dùng để ưu tiên xử lý.

### B01 — Trang Liên hệ thiếu view

- **Mức độ:** Cao. **Trạng thái:** Mở.
- **Tái hiện:** truy cập `/contact`.
- **Mong đợi:** hiển thị thông tin liên hệ và form hỗ trợ.
- **Thực tế:** controller require `views/lien_he/lien_he.php` nhưng file không tồn tại; xuất hiện Warning và Fatal error.
- **Ảnh hưởng:** không sử dụng được trang Liên hệ ở cả 4 kích thước đã thử.
- **Cần xử lý:** bổ sung/khôi phục đúng view và kiểm tra lại validation, gửi form, lưu liên hệ.

### B02 — Trang Yêu thích thiếu view

- **Mức độ:** Cao. **Trạng thái:** Mở.
- **Tái hiện:** đăng nhập tài khoản kiểm thử, mở `/wishlist`.
- **Mong đợi:** hiển thị danh sách yêu thích hoặc trạng thái rỗng.
- **Thực tế:** thiếu `views/tai_khoan/yeu_thich.php`; trang lỗi dù model đã được đặt đúng vị trí.
- **Ảnh hưởng:** không sử dụng được màn hình danh sách yêu thích.
- **Cần xử lý:** bổ sung view; kiểm tra danh sách rỗng, thêm/bỏ yêu thích và trạng thái sau tải lại.

### B03 — Tra cứu đơn chưa xác minh số điện thoại

- **Mức độ:** Cao. **Trạng thái:** Mở.
- **Tái hiện:** dùng đơn QA riêng; đăng xuất; tra cứu chỉ bằng mã đơn, không cung cấp số điện thoại.
- **Mong đợi:** kiểm tra mã đơn và số điện thoại khớp trước khi trả thông tin giao hàng theo yêu cầu trong bản phân công.
- **Thực tế:** chỉ với mã đơn đã xem được tên, điện thoại và địa chỉ giao hàng.
- **Ảnh hưởng:** thông tin đơn có thể được trả cho người chưa được xác minh theo yêu cầu.
- **Cần xử lý:** yêu cầu hai thông tin và kiểm tra khớp; thử mã đúng/SĐT sai, mã sai/SĐT đúng và hai giá trị đúng; giới hạn dữ liệu trả về phù hợp.

### B04 — Liên kết nội dung chân trang trả 404

- **Mức độ:** Trung bình. **Trạng thái:** Mở.
- **Tái hiện:** mở `/about`, `/news`, `/recruit`, `/store`, `/policy/shipping`, `/policy/return`, `/policy/warranty`, `/policy/payment`, `/policy/privacy`.
- **Mong đợi:** có trang nội dung tương ứng hoặc điều hướng phù hợp.
- **Thực tế:** cả 9 URL trả 404.
- **Cần xử lý:** bổ sung các trang nội dung hoặc điều chỉnh liên kết; kiểm tra lại điều hướng.

### B05 — Thiếu ảnh đại diện mặc định

- **Mức độ:** Thấp. **Trạng thái:** Mở.
- **Tái hiện:** đăng nhập tài khoản chưa có avatar, mở `/account`, xem khu vực chỉnh sửa ảnh đại diện.
- **Mong đợi:** hiển thị ảnh mặc định hoặc fallback hợp lệ.
- **Thực tế:** `assets/images/no-avatar.png` không tồn tại, tạo ảnh lỗi.
- **Cần xử lý:** bổ sung tài nguyên mặc định hoặc fallback phù hợp; kiểm tra cả tài khoản có/không có avatar.

## 8. Dữ liệu sau kiểm thử

- Đã đăng xuất tài khoản QA và dọn 1 người dùng QA, 2 đơn QA cùng các bản ghi con phát sinh cho tài khoản thử.
- Kiểm tra sau dọn trả về 0 người dùng QA và 0 đơn của tài khoản QA.
- Các fixture dùng để mở màn hình không điều chỉnh tồn kho; không thực hiện giao dịch thanh toán hoặc gửi email.
- Không sửa cấu trúc bảng trong phiên QA. Bộ đếm AUTO_INCREMENT có thể đã tăng khi chèn dữ liệu thử.
- Mở trang chi tiết kích hoạt `incrementView` có sẵn, nên `san_pham.luot_xem` tăng theo logic ứng dụng. Không có mốc lượt xem trước thử để khôi phục chính xác.
- Khi kiểm thử lại các ca đơn hàng cần tạo dữ liệu riêng mới; các đơn QA của phiên này đã được dọn.

## 9. Phạm vi chưa xác nhận

- Luồng submit tạo đơn đầu cuối, transaction và trừ kho.
- Giao dịch COD/chuyển khoản/ví ở đầu cuối và gửi email xác nhận.
- Đăng ký qua email, quên/đặt lại mật khẩu qua email, Google OAuth.
- Upload avatar và thao tác thêm/sửa/xóa dữ liệu quản trị.
- Đăng nhập admin bằng mật khẩu hợp lệ: các trang quản trị đã được mở bằng cơ chế tự đăng nhập localhost có sẵn; form login được kiểm tra hiển thị riêng.
- Độ chính xác đầy đủ của số liệu báo cáo theo nhiều tập dữ liệu thực tế.
- Nhiều trình duyệt, thiết bị di động thật, kiểm thử tải và rà soát bảo mật toàn diện.

## 10. Việc cần làm tiếp

1. Xử lý B01, B02 và B03; kiểm thử lại các bước tái hiện và trường hợp dữ liệu sai.
2. Thống nhất các file dùng chung và hai đường dẫn sao chép với thành viên phụ trách trước khi ghép thay đổi code.
3. Xử lý B04, B05 và chạy lại ma trận hiển thị trên bản đã tích hợp.
4. Bổ sung kiểm thử tạo đơn đầu cuối trong môi trường thử tách biệt, kiểm tra stock/transaction/email và các luồng xác thực còn thiếu.
5. Chỉ cập nhật trạng thái lỗi sang đã sửa sau khi kiểm thử lại; ghi commit SHA của bản tích hợp khi repository đã có lịch sử Git.

## Phụ lục — Đối chiếu và kiểm tra bản tích hợp

Phiên kiểm thử ban đầu thực hiện trên bản sao dự án chưa có `.git`. Khi chuẩn bị tích hợp, đã clone repository và ghép các đoạn sửa lên nhánh `qa/thao-responsive-report`, xuất phát từ `origin/main` tại commit `acfc7a05659f2e5e7973d551e141c1bac6ae8736`.

Các commit mã nguồn được tách riêng để nhóm review:

| Nhóm thay đổi | Commit |
| --- | --- |
| Restore required MVC file locations | [`27a3f65`](https://github.com/Lyphan04/Congnghephanmem/commit/27a3f653caefa6d44a12f42799e0aafcd372f349) |
| Routing and local installation paths | [`6dc858d`](https://github.com/Lyphan04/Congnghephanmem/commit/6dc858d3543ed592c39d9affb83a8170a0be54dd) |
| Responsive product filters | [`0bf94a6`](https://github.com/Lyphan04/Congnghephanmem/commit/0bf94a6e3f1c78aea2ffdb9858b52cb1bfca469c) |

Báo cáo được lưu trong một commit tài liệu riêng sau các commit mã nguồn. Các commit trước đó của nhóm được giữ nguyên trong lịch sử; nhánh thay đổi được đề nghị review qua Pull Request trước khi hợp nhất.

Trên bản clone đã ghép, 68 file PHP tiếp tục qua `php -l` và 13 kiểm tra HTTP/API bổ sung đều đạt. Các kiểm tra này bao gồm trang chủ, danh sách, chi tiết sản phẩm, giỏ, 404, JSON tìm kiếm/API lạ và chuyển hướng yêu cầu đăng nhập. Đây là đợt kiểm tra tích hợp bổ sung, không được cộng vào 128 lượt hiển thị của phiên QA ban đầu.

Kiểm tra HTTP bổ sung chạy bằng PHP development server trên loopback; server này không nạp `.htaccess`. Cấu hình Apache đã được kiểm tra trong phiên QA trên XAMPP trước đó. Nội dung 8 file mã nguồn được đối chiếu khớp bản local đã thử, bỏ qua khác biệt ký tự xuống dòng. Các lỗi mở tại mục 7 vẫn cần xử lý.
