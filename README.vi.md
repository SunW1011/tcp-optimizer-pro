<p align="center"><a href="https://github.com/SunW1011/tcp-optimizer-pro">English</a> | <strong>Tiếng Việt</strong></p>

# TCP Optimizer Pro v2.2.3

TCP Optimizer Pro là mô-đun KernelSU cho Android ARM64 (API 26 trở lên, `versionCode=223`). Mô-đun áp dụng cấu hình TCP và Qdisc cho Wi-Fi và dữ liệu di động, rồi đọc lại giá trị do kernel báo. Thuật toán có sẵn và khả năng đổi hàng đợi phụ thuộc vào kernel và driver mạng.

## Cài đặt

1. Tải `TCP-Optimizer-Pro-v2.2.3-KSU.zip` và `SHA256SUMS` từ [bản phát hành v2.2.3](https://github.com/SunW1011/tcp-optimizer-pro/releases/tag/v2.2.3).
2. Trong thư mục tải xuống, chạy `sha256sum -c SHA256SUMS` và kiểm tra dòng kết quả của ZIP có ghi `OK`.
3. Cài ZIP trong KernelSU Manager, khởi động lại thiết bị rồi mở WebUI của mô-đun.

## Cấu hình nhanh theo mục tiêu

Tab **Cài đặt** có ba hồ sơ cho Wi-Fi và dữ liệu di động. Cả ba đặt TCP và Qdisc về **Tự động** và bật khởi tạo Qdisc lúc boot. TCP được thử theo thứ tự `bbr3 → bbr2 → bbr → cubic → westwood → htcp → reno`. Qdisc ưu tiên FQ với BBR và FQ-CoDel với các thuật toán TCP khác.

| Hồ sơ | Thiết lập |
| --- | --- |
| Tối đa tốc độ | Bật cửa sổ TCP khởi tạo cân bằng và giữ cửa sổ gửi sau khi rảnh trong các chế độ phù hợp. |
| Chơi game / Độ trễ thấp | Bật các tùy chọn độ trễ thấp tạm thời khi màn hình hoạt động và nhiệt pin dưới ngưỡng. |
| Cân bằng & Tiết kiệm pin | Giữ mặc định ROM, bật Auto nền và bảo vệ TSQ/Lowat, tắt các lease độ trễ thấp. |

Cả ba giữ mặc định ROM và giữ chế độ vận hành bạn đã chọn. Thông lượng thực tế còn phụ thuộc vào đường truyền và băng thông phía nhà mạng. Các lease TCP có thể hoạt động ở **Chơi game** hoặc **Tải nhanh**, kể cả khi **Tự động** chọn một trong hai chế độ này lúc chạy nền. Trên thiết bị hỗ trợ, mở WebUI để bắt đầu lease tạm tắt tiết kiệm điện Wi-Fi trong chế độ Chơi game. Daemon nhả lease khi tắt màn hình, đường truyền yếu hoặc pin chạm ngưỡng nhiệt.

## Wi-Fi kép

Khi hai giao diện Wi-Fi cùng định tuyến, mô-đun hoàn nguyên cửa sổ TCP đã đổi trên Wi-Fi và nhả lease tạm tắt tiết kiệm điện Wi-Fi của chế độ **Chơi game**. Sau 15 giây dùng Wi-Fi đơn, mô-đun áp lại cửa sổ đã chọn kể cả khi WebUI đóng. Dữ liệu di động và các lease chỉ đổi TCP vẫn theo điều kiện thông thường.

WebUI hiện **Tự tạm hoãn (Wi-Fi kép)** trong thời gian chờ. Độ ổn định Wi-Fi còn phụ thuộc ROM, driver và điểm phát.

## Kiểm tra mạng

- Chọn giao diện **Sáng** trong WebUI để giữ nền sáng ngay cả khi Android đang dùng giao diện tối.
- Khi WebUI báo chờ tạo lại hàng đợi MQ bằng FQ, giữ bật **Khởi tạo Qdisc Wi-Fi lúc boot** và khởi động lại. WebUI báo riêng nếu công tắc này đang tắt.
- Từ điển kernel hiển thị 32 sysctl và đánh dấu những giá trị chưa đọc được. Điểm Bufferbloat tính cả độ trễ khi có tải và tỷ lệ mất gói. Khi so sánh A/B, dùng cùng loại mạng, phép đo và đích.
- Nếu DNS tự động dùng địa chỉ router nội bộ, chọn Cloudflare, Google hoặc AdGuard để kiểm tra Private DNS qua TCP/853.

## Sao lưu và chẩn đoán

Trong tab **Cài đặt**, nhập tên tệp JSON rồi chọn thư mục để xuất hoặc nhập cấu hình. Thư mục mặc định là `/sdcard/Download`. Bạn cũng có thể dùng trình chọn tệp của thiết bị để nhập JSON. Sau khi nhập, xem mục **Xác nhận kernel** để biết kết quả áp dụng.

Báo cáo chẩn đoán dùng cùng các lựa chọn thư mục và được lưu dưới dạng TXT. WebUI hỏi trước khi ghi đè và hiện đường dẫn khi Android cung cấp.

## Khôi phục và báo lỗi

Chọn **Khôi phục gốc** để dừng tối ưu và khôi phục các giá trị đã ghi nhận trong phiên khởi động hiện tại. Xem kết quả đọc lại để biết các thay đổi còn sót hoặc xung đột.

Khi [báo lỗi](https://github.com/SunW1011/tcp-optimizer-pro/issues), ghi phiên bản mô-đun, phiên bản Android, mẫu máy và các bước tái hiện. Có thể xuất báo cáo chẩn đoán trong WebUI.

Xem [changelog](https://github.com/SunW1011/tcp-optimizer-pro/blob/main/changelog.md) để tra lịch sử phát hành.
