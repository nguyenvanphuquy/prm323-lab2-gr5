# Design Brief — Expense Tracker

**Lab 2 · Nhóm GR5 · Phiên bản 1.0 trước khi dựng giao diện trên Google Stitch**

## 1. Mục tiêu thiết kế

Thiết kế ứng dụng quản lý thu chi trên điện thoại bằng tiếng Việt. Ưu tiên Nguyễn Minh Anh (P01), sinh viên muốn ghi khoản chi ngay sau khi thanh toán. Trên Trang chủ, người dùng cần thấy ngay ngân sách tháng còn lại và nút **Thêm khoản chi**. Mục tiêu kiểm thử là tự lưu khoản ăn trưa 45.000 VNĐ trong tối đa 15 giây.

Với Ngọc Linh (P02), màn Thống kê giúp xác định danh mục chi nhiều nhất trong tháng và mở danh sách khoản chi của danh mục đó. Với Quốc Huy (P03), màn Ngân sách cho thấy hạn mức, số đã chi và số còn lại của từng danh mục.

Nguồn nội bộ — [Persona](../ux/persona.md) và [User Flow](../ux/user-flow.md).

## 2. Màu sắc

Dùng giao diện sáng, nền xám nhạt và thẻ trắng. Xanh lam dành cho điều hướng và thao tác chính. Màu trạng thái luôn đi kèm nhãn, biểu tượng hoặc dấu cộng/trừ.

| Token | HEX | Cách dùng |
|---|---|---|
| Primary | `#1D4ED8` | Nút chính, tab đang chọn, viền khi focus |
| On primary / Surface | `#FFFFFF` | Chữ trên nút chính, nền thẻ và ô nhập |
| Primary tint | `#EFF6FF` | Nền mục đang chọn và thẻ ngân sách nổi bật |
| Background | `#F8FAFC` | Nền toàn màn hình |
| Text primary | `#0F172A` | Tiêu đề, số tiền, nội dung chính |
| Text secondary | `#475569` | Mô tả, ghi chú, ngày giao dịch |
| Divider | `#E2E8F0` | Đường phân cách thẻ và danh sách |
| Control border | `#64748B` | Viền mặc định của ô nhập |
| Success / Income | `#166534` | Xác nhận lưu, khoản thu |
| Warning | `#92400E` | Ngân sách sắp chạm hạn mức |
| Error / Expense | `#B91C1C` | Lỗi nhập liệu, khoản chi, vượt hạn mức |

Mục tiêu tương phản cho chữ là tối thiểu 4,5:1 trên nền thực tế. Kiểm tra lại màu trên các màn đã dựng trước khi bàn giao prototype.

## 3. Kiểu chữ và định dạng

Dùng **Inter** với bộ ký tự tiếng Việt. Nếu công cụ dựng không có Inter hỗ trợ tiếng Việt, dùng **Roboto** đồng nhất trên toàn bộ màn hình. Dùng chữ số có chiều rộng đồng đều nếu font hỗ trợ.

| Kiểu | Cỡ / dòng | Độ đậm | Áp dụng |
|---|---|---|---|
| Số tiền nổi bật | 32 / 40 | 700 | Ngân sách còn lại, tổng chi danh mục |
| Tiêu đề màn hình | 24 / 32 | 700 | Trang chủ, Thống kê, Ngân sách |
| Tiêu đề nhóm | 18 / 24 | 600 | Chi tiêu hôm nay, giao dịch gần đây |
| Nội dung | 16 / 24 | 400 | Mô tả, nội dung nhập, nhãn danh sách |
| Nút và nhãn ô nhập | 14 / 20 | 600 | Lưu giao dịch, Số tiền |
| Chú thích | 12 / 16 | 500 | Ngày giao dịch, nhãn thanh điều hướng |

Các giá trị trên là sp khi triển khai và dùng cùng giá trị số trong khung thiết kế. Hiển thị tiền như **45.000 VNĐ**, danh sách dùng **−45.000 VNĐ** cho khoản chi và dấu **+** cho khoản thu. Căn phải cột số tiền. Ngày hiển thị theo `dd/MM/yyyy`, tháng theo `MM/yyyy`. Khi tăng cỡ chữ, cho phép nhãn xuống dòng và vùng nội dung cuộn.

## 4. Bố cục và khoảng cách

- Dùng khung thiết kế tham chiếu **390 × 844**, bố cục một cột và tôn trọng vùng an toàn của thiết bị.
- Dùng thang khoảng cách **4, 8, 12, 16, 24, 32 dp**. Lề ngang mặc định 16 dp. Cách giữa các nhóm 24 dp. Padding thẻ 16 dp. Icon cách nhãn 8 dp.
- Bo góc thẻ 16 dp, nút và ô nhập 12 dp. Icon nét đơn 24 dp, vùng chạm tối thiểu **48 × 48 dp**.
- Thanh điều hướng dưới xuất hiện trên S01, S03, S05, S07 theo thứ tự **Trang chủ · Lịch sử · Thống kê · Ngân sách**. Mục hiện tại có icon, nhãn và nền chọn. Các màn con dùng nút **Quay lại** ở thanh trên.
- Nút chính trong biểu mẫu chiếm toàn chiều rộng nội dung. Khi mở bàn phím, nội dung cuộn được để người dùng thấy trường đang nhập, lỗi và nút lưu.

## 5. Quy tắc component

| Component | Quy tắc |
|---|---|
| Nút chính | Cao tối thiểu 48 dp, nền Primary, chữ trắng. Mỗi màn hình có tối đa một nút chính. Dùng nhãn chỉ rõ kết quả như **Thêm khoản chi**, **Lưu giao dịch**, **Lưu ngân sách**. Khi đang lưu, hiện **Đang lưu…** và khóa thao tác lặp. |
| Nút phụ | Nền trắng hoặc trong suốt, chữ Primary. **Hủy** là thao tác phụ trên S08. Giữ vùng chạm tối thiểu 48 dp. |
| Ô nhập số tiền | Nhãn cố định **Số tiền** hoặc **Hạn mức**, hậu tố **VNĐ**, bàn phím số, chiều cao tối thiểu 52 dp. Số nhập phải lớn hơn 0. Lỗi nằm dưới trường và giữ nguyên dữ liệu ở các trường khác. |
| Chọn danh mục, ngày và tháng | Dùng ô có nhãn, giá trị hiện tại và icon phù hợp. Trường chưa chọn hiện **Chọn danh mục**. Trường bắt buộc thiếu dữ liệu hiện lỗi cạnh trường sau khi bấm lưu. |
| Thẻ tổng quan | Nhãn phía trên, số tiền nổi bật phía dưới. Trên S01 đặt **Ngân sách tháng còn lại** ở đầu nội dung và nút **Thêm khoản chi** ngay sau phần tổng quan. |
| Hàng giao dịch | Icon và danh mục bên trái, ghi chú nếu có, số tiền bên phải. Lịch sử nhóm theo ngày. Chạm toàn hàng để mở chi tiết giao dịch. |
| Biểu đồ danh mục | Dùng thanh ngang sắp theo tổng chi giảm dần. Mỗi hàng có tên danh mục và số tiền bằng chữ, đồng thời mở được S06. Khi đổi tháng, cập nhật số tổng hợp và các thanh theo cùng kỳ. |
| Thẻ ngân sách | Hiển thị tên danh mục, **Hạn mức**, **Đã chi**, **Còn lại** và thanh tiến độ. Đề xuất cho prototype dùng trạng thái **Trong hạn mức** dưới 80%, **Sắp chạm hạn mức** từ 80% đến dưới 100%, **Đã chạm hạn mức** tại 100% và **Vượt hạn mức** trên 100%. Thanh dừng ở 100%, nhãn cho biết số tiền vượt. |
| Phản hồi và trạng thái trống | Khi lưu thành công, hiện thông báo ngắn và cập nhật dữ liệu tại màn đích. Với tháng chưa có khoản chi, hiển thị trạng thái trống ngay trên S05 và giữ bộ lọc tháng để người dùng đổi kỳ. |

## 6. Giọng điệu và nội dung

Dùng câu ngắn, trực tiếp, tập trung vào thao tác tiếp theo. Giữ cùng một nhãn cho cùng một thao tác ở các màn hình.

| Tình huống | Nội dung hiển thị |
|---|---|
| Số tiền trống | Nhập số tiền. |
| Số tiền không hợp lệ | Nhập số tiền lớn hơn 0 VNĐ. |
| Thiếu danh mục | Chọn một danh mục. |
| Lưu giao dịch thành công | Đã lưu khoản chi 45.000 VNĐ. |
| Tháng chưa có dữ liệu | Chưa có khoản chi trong tháng này. Chọn tháng khác để xem thống kê. |
| Vượt hạn mức | Vượt hạn mức 150.000 VNĐ. |

## 7. Phạm vi dựng trên Stitch

| Luồng | Màn hình | Nội dung cần thể hiện |
|---|---|---|
| UF-01 · Ghi khoản chi | S01 Trang chủ, S02 Thêm giao dịch | S02 mở sẵn loại **Khoản chi**, ngày mặc định là hôm nay, ghi chú tùy chọn. Dựng trường hợp lỗi số tiền hoặc danh mục. Sau khi lưu 45.000 VNĐ vào **Ăn uống**, S01 đổi ngân sách còn lại từ **1.200.000 VNĐ** thành **1.155.000 VNĐ**. |
| UF-01 · Kiểm tra giao dịch | S03 Lịch sử giao dịch, S04 Chi tiết giao dịch | Giao dịch mới xuất hiện đúng ngày. Chi tiết có số tiền, loại giao dịch, danh mục, ngày và ghi chú nếu có. |
| UF-02 · Xem chi tiêu | S05 Thống kê, S06 Chi tiêu theo danh mục | S05 có tổng thu chi, bộ lọc tháng, biểu đồ và biến thể tháng trống. S06 giữ danh mục và tháng đã chọn, hiển thị tổng chi và danh sách khoản chi tương ứng. |
| UF-03 · Đặt hạn mức | S07 Ngân sách, S08 Tạo ngân sách danh mục | S08 có tháng, danh mục, hạn mức, nút **Lưu ngân sách** và **Hủy**. Sau khi lưu hạn mức **3.000.000 VNĐ** cho **Ăn uống**, S07 hiển thị đã chi **450.000 VNĐ**, còn lại **2.550.000 VNĐ**. Hủy trở về S07 và bỏ dữ liệu đang nhập. |

Dựng S01 và S02 trước để xác lập bố cục và component cho luồng chính, sau đó áp dụng cùng quy tắc cho S03–S08. Thông báo, lỗi và trạng thái trống là biến thể của màn tương ứng. Kiểm tra đủ ba luồng sau khi nối prototype, với mục tiêu 15 giây cho ghi khoản chi, 30 giây cho xem báo cáo và 2 phút cho tạo hạn mức. Ghi nguyên văn prompt đầu tiên và lưu ảnh kết quả Stitch vào hồ sơ thiết kế theo hướng dẫn của Lab 2.
