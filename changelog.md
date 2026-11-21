## TCP Optimizer Pro v1.9.0

- Mở chẩn đoán Wi-Fi từ thẻ Trang chủ và xem trạng thái DNS riêng tư.
- Chọn đích đo độ trễ hoặc kiểm tra TCP/853 theo yêu cầu.
- Thu gọn chẩn đoán tuyến mạng, trạng thái xác nhận kernel và dòng ưu tiên ứng dụng.

# TCP Optimizer Pro v1.8.1

- Header WebUI hiển thị phiên bản đọc từ trạng thái daemon.
- Hộp thoại TCP + Qdisc giải thích thuật toán và hàng đợi thực tế khi chọn Auto.
- Chọn chế độ CAKE Diffserv bằng nhóm nút theo màu giao diện Bento.

# TCP Optimizer Pro v1.8.0

- Lease Wi-Fi tùy chọn cho chế độ Chơi game. Hai lease TCP tùy chọn cho Chơi game và Tốc độ tối đa. Module kiểm tra màn hình và nhiệt pin khi giữ lease, rồi khôi phục giá trị trong journal nếu điều kiện thay đổi.
- Tùy chọn initcwnd/initrwnd xác minh và ghi riêng tuyến mặc định IPv4 và IPv6 trên giao diện egress hiện tại. Các tuyến CLAT khác giao diện và tuyến không xác định duy nhất được bỏ qua.
- Danh sách Qdisc nhận PIE và FQ-PIE khi kernel báo hỗ trợ. Tham số nâng cao tùy chọn gồm quantum theo MTU cho FQ/FQ-CoDel và Diffserv cho CAKE trong các chế độ chọn tay.
- Popup Wi-Fi hiển thị Power Save thực tế, trạng thái lease, độ rộng kênh, tần số, băng tần và mã vùng do driver cung cấp.
- Thêm metadata OTA KernelSU Next và workflow tạo GitHub Release từ tag đã qua kiểm thử.

Cấu hình mới mặc định tắt các lease, cửa sổ tuyến và tham số Qdisc nâng cao. Nâng cấp giữ cấu hình người dùng đã lưu.
