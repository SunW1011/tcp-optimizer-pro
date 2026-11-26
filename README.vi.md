<p align="center"><a href="https://github.com/SunW1011/tcp-optimizer-pro">English</a> | <strong>Tiếng Việt</strong></p>

# TCP Optimizer Pro v2.5.2

TCP Optimizer Pro là module KernelSU cho Android ARM64 (API 26 trở lên, `versionCode=252`). Module áp dụng cấu hình TCP và Qdisc cho Wi-Fi và dữ liệu di động, rồi đọc lại giá trị do kernel báo. Thuật toán có sẵn và khả năng đổi hàng đợi phụ thuộc vào kernel và driver mạng.

## WebUI

Trang chủ hiển thị kết nối đang dùng, hai cấu hình mạng, bốn thông số TCP và bốn giá trị nhiệt độ. Mở thanh tuyến mạng để xem chẩn đoán IPv4, IPv6 và thông tin thiết bị. Chạm vào nhiệt độ để xem tên cảm biến. Chi tiết ô Pin có thêm ngưỡng bảo vệ đang áp dụng.

Trong **Cài đặt → Nâng cao**, thanh nhiệt hiển thị nhiệt độ pin và hai ngưỡng bảo vệ. Dùng nút tăng giảm, mốc nhanh hoặc lưới bốn cột để đổi ngưỡng gốc. Lưới có các mốc từ 35.0°C đến 50.0°C, cách nhau 0.5°C. Khi sạc, ngưỡng tăng thêm 2°C. Trong **Cài đặt → Mạng**, cảnh báo **Driver giữ MQ** cho biết driver giữ nguyên cây hàng đợi. Tự động và `fq` vẫn chọn được.

Tab Ứng dụng hiển thị tên và biểu tượng thật khi trình quản lý cung cấp dữ liệu. Nếu môi trường có công cụ đọc APK, WebUI có thể lấy tên từ metadata của APK. Khi thiếu dữ liệu tương ứng, WebUI dùng tên gói rút gọn hoặc chữ cái đầu.

## Cài đặt

1. Tải `TCP-Optimizer-Pro-v2.5.2-KSU.zip` và `SHA256SUMS` từ [bản phát hành v2.5.2](https://github.com/SunW1011/tcp-optimizer-pro/releases/tag/v2.5.2).
2. Trong thư mục tải xuống, chạy `sha256sum --ignore-missing -c SHA256SUMS` và kiểm tra dòng kết quả của ZIP có ghi `OK`.
3. Cài ZIP trong KernelSU Manager, khởi động lại thiết bị rồi mở WebUI của module.

### Ứng dụng Companion

ZIP của module đã kèm Companion. Sau khi cài ZIP, khởi động lại rồi bấm **Action** trong trình quản lý. Ứng dụng kết nối khi ở tiền cảnh. Nếu ứng dụng báo chưa kết nối, mở WebUI của module. Khởi động lại với cùng phiên bản sẽ giữ lựa chọn gỡ Companion. Bấm **Action** để cài lại hoặc cập nhật cho người dùng chính. Có thể dùng APK rời đã kiểm tra SHA-256. Nhập và xuất cấu hình dùng trình chọn tệp Android.

## Cấu hình nhanh theo mục tiêu

Tab **Cài đặt** có ba hồ sơ cho Wi-Fi và dữ liệu di động. Cả ba đặt TCP và Qdisc về **Tự động** và bật khởi tạo Qdisc lúc boot. TCP được thử theo thứ tự `bbr3 → bbr2 → bbr → cubic → westwood → htcp → reno`. Qdisc ưu tiên FQ với BBR và FQ-CoDel với các thuật toán TCP khác.

| Hồ sơ | Thiết lập |
| --- | --- |
| Tối đa tốc độ | Bật cửa sổ TCP khởi tạo cân bằng và giữ cửa sổ gửi sau khi rảnh trong các chế độ phù hợp. |
| Chơi game / Độ trễ thấp | Bật các tùy chọn độ trễ thấp tạm thời khi màn hình hoạt động và nhiệt pin dưới ngưỡng. |
| Cân bằng & Tiết kiệm pin | Giữ mặc định ROM, bật Auto nền và bảo vệ TSQ/Lowat, tắt các lease độ trễ thấp. |

Cả ba giữ mặc định ROM và giữ chế độ vận hành bạn đã chọn. Thông lượng thực tế còn phụ thuộc vào đường truyền và băng thông phía nhà mạng. Các lease TCP có thể hoạt động ở **Chơi game** hoặc **Tải nhanh**, kể cả khi **Tự động** chọn một trong hai chế độ này lúc chạy nền. Trên thiết bị hỗ trợ, mở WebUI để bắt đầu lease tạm tắt tiết kiệm điện Wi-Fi trong chế độ Chơi game. Daemon nhả lease khi tắt màn hình, đường truyền yếu hoặc pin chạm ngưỡng nhiệt.

## Wi-Fi kép

Khi hai giao diện Wi-Fi cùng định tuyến, module hoàn nguyên cửa sổ TCP đã đổi trên Wi-Fi và nhả lease tạm tắt tiết kiệm điện Wi-Fi của chế độ **Chơi game**. Sau 15 giây dùng Wi-Fi đơn, module áp lại cửa sổ đã chọn kể cả khi WebUI đóng. Dữ liệu di động và các lease chỉ đổi TCP vẫn theo điều kiện thông thường.

WebUI hiện **Tự tạm hoãn (Wi-Fi kép)** trong thời gian chờ. Độ ổn định Wi-Fi còn phụ thuộc ROM, driver và điểm phát.

## VPN và tunnel

Khi VPN có tuyến đang hoạt động, daemon tạm hoãn chỉnh cửa sổ TCP khởi tạo trên Wi-Fi và di động. Daemon hoàn nguyên các thông số tuyến IPv4 và IPv6 đã chỉnh, đồng thời giữ nguyên tuyến của tunnel. Sau khi VPN ngắt, daemon chờ 5 giây rồi áp lại trên tuyến đủ điều kiện. Trang chính và báo cáo chẩn đoán hiển thị trạng thái tạm hoãn.

## Kiểm tra mạng

- Chọn giao diện **Sáng** trong WebUI để giữ nền sáng ngay cả khi Android đang dùng giao diện tối.
- Khi WebUI báo chờ tạo lại hàng đợi MQ bằng FQ, giữ bật **Khởi tạo Qdisc Wi-Fi lúc boot** và khởi động lại. WebUI báo riêng nếu công tắc này đang tắt.
- Từ điển kernel hiển thị 32 sysctl và đánh dấu những giá trị chưa đọc được. Điểm Bufferbloat tính cả độ trễ khi có tải và tỷ lệ mất gói. Khi so sánh A/B, dùng cùng loại mạng, phép đo và đích.
- Nếu DNS tự động dùng địa chỉ router nội bộ, chọn Cloudflare, Google hoặc AdGuard để kiểm tra Private DNS qua TCP/853.

## Sao lưu và chẩn đoán

Trang **Cài đặt** mở ở tab **Mạng**. Tab **Nâng cao** chứa các tùy chọn daemon, định tuyến, Qdisc và ghi đè ROM. Vào **Hệ thống** để xem kết quả kernel, sao lưu cấu hình, xuất chẩn đoán hoặc tra cứu tham số.

Trong tab **Hệ thống**, bấm **Xuất cấu hình** để lưu bản sao JSON. **Nhập cấu hình** yêu cầu xác nhận trước khi mở trình chọn tệp Android. Sau khi nhập, xem kết quả ở mục **Xác nhận kernel**.

**Xuất cấu hình** và **Lưu tệp** trong cửa sổ xem báo cáo dùng cùng một hộp thoại. Hộp thoại mở ở `/sdcard/Download` hoặc ở `/sdcard` nếu chưa có thư mục Download. Chạm vào thư mục để mở, **←** để lên thư mục cha hoặc **+** để tạo thư mục. Bấm **×** cạnh tên tệp để xóa tên gợi ý. WebUI hỏi trước khi ghi đè và hiện đường dẫn đầy đủ sau khi lưu.

Trang **Ứng dụng** hiển thị biểu tượng khi trình quản lý KernelSU cung cấp ảnh và dùng chữ cái đầu nếu ảnh không tải được. Trong **Hệ thống**, mục **Cộng đồng & Ủng hộ** có liên kết GitHub, Telegram và mã QR ngân hàng, USDT dùng ngoại tuyến.

## Khôi phục và báo lỗi

Chọn **Khôi phục gốc** để dừng tối ưu và khôi phục các giá trị đã ghi nhận trong phiên khởi động hiện tại. Xem kết quả đọc lại để biết các thay đổi còn sót hoặc xung đột.

Khi [báo lỗi](https://github.com/SunW1011/tcp-optimizer-pro/issues), ghi phiên bản module, phiên bản Android, mẫu máy và các bước tái hiện. Có thể xuất báo cáo chẩn đoán trong WebUI.

Xem [changelog](https://github.com/SunW1011/tcp-optimizer-pro/blob/main/changelog.md) để tra lịch sử phát hành.
