# DIY Flat Panel

DIY Flat Panel là Flat Panel / Cover Controller dùng ESP32. Sản phẩm mặc định được điều khiển bằng **website tích hợp sẵn trong box**; không cần cài ứng dụng để sử dụng hằng ngày.

## Chọn cách điều khiển

### Website — cách dùng mặc định

Website dùng được trên iPhone, iPad, Android, Windows, macOS, TV và mọi thiết bị có trình duyệt.

- Khi kết nối vào Wi-Fi của Flat Panel (AP mode), mở: `http://192.168.4.1`
- Khi Flat Panel đã kết nối Wi-Fi nhà (Station mode), mở: `http://flatpanel.local`

Website có điều khiển Main Cover, Scope Cover (nếu có), đèn Flat Panel, độ sáng, Auto Open, Auto Close, cấu hình servo, Wi-Fi Station và cập nhật firmware.

### Ứng dụng Android — tùy chọn

Ứng dụng Android dành cho người dùng muốn điều khiển bằng app thay vì website. Không bắt buộc phải cài.

### Driver ASCOM — dành cho N.I.N.A.

Driver ASCOM dành cho người dùng muốn điều khiển Main Cover và Flat Panel Light từ N.I.N.A. trên Windows.

## Tải xuống

- [Firmware ESP32 1.3.16 — dùng để cập nhật OTA](./FlatPanel-1.3.16-ota.bin)
- [Firmware ESP32 1.3.16 — ảnh flash đầy đủ 4 MB](./FlatPanel-1.3.16-merged.bin)
- [Ứng dụng Android 2.6](./DIY-Flat-Panel-Android-2.6.apk)
- [DIY Flat Panel ASCOM Driver 1.0.17](./DIY-Flat-Panel-ASCOM-Setup-1.0.17.exe)

## Bắt đầu bằng website

1. Cấp nguồn cho DIY Flat Panel.
2. Trên điện thoại hoặc máy tính, kết nối Wi-Fi `FlatPanel_v1` nếu box chưa được cấu hình Wi-Fi nhà.
3. Mở `http://192.168.4.1`.
4. Trong tab **Configure**, có thể cấu hình Wi-Fi Station để lần sau mở nhanh bằng `http://flatpanel.local`.

Nếu box chỉ có Main Cover, tắt **Scope Cover installed** trong tab Configure. Thiết lập này được lưu trong box và Scope Cover sẽ được ẩn đi.

## Dùng ứng dụng Android

1. Tải và cài file APK Android ở trên.
2. Lần cài đầu, Android có thể yêu cầu cho phép **Install unknown apps**.
3. Kết nối điện thoại với Flat Panel qua AP hoặc cùng Wi-Fi Station, rồi mở app và kết nối thiết bị.

## Dùng với N.I.N.A.

1. Đóng N.I.N.A. và chạy file cài **DIY Flat Panel ASCOM Driver** bằng quyền Administrator.
2. Mở N.I.N.A., tại Flat Panel chọn **Viet DIY Flat Panel**.
3. Kết nối box với PC qua USB và Connect trong N.I.N.A.
4. Nút bánh răng của driver mở Setup để chỉnh góc Open/Closed và tốc độ Main Cover.

Setup tự đọc cấu hình servo từ box. **Save & Apply** chỉ bật khi có thay đổi, nhằm tránh vô tình ghi đè cấu hình đã tinh chỉnh. Scope Cover là app/web-only và không được N.I.N.A. điều khiển.

## Cập nhật firmware

Cách khuyến nghị là cập nhật từ website khi Flat Panel đang ở **Station mode**:

1. Mở `http://flatpanel.local`.
2. Vào **Configure** → **Firmware Update**.
3. Kiểm tra bản mới và xác nhận cập nhật.
4. Giữ nguyên nguồn và Wi-Fi cho tới khi box tự khởi động lại.

Driver ASCOM cũng có công cụ cập nhật qua cáp USB trong Setup → **Firmware Update**.

Nếu dùng N.I.N.A./ASCOM, hãy cài **ASCOM Driver 1.0.17** trước khi cập nhật box lên firmware 1.3.11. Driver 1.0.16 chỉ dùng serial 9600 baud nên không kết nối lại được sau khi firmware mới đã chuyển sang 115200 baud.

### Nếu flash firmware thủ công, chọn đúng file firmware

- `FlatPanel-*-ota.bin`: chỉ dùng cho cập nhật OTA. Không flash file này tại địa chỉ `0x0`.
- `FlatPanel-*-merged.bin`: ảnh flash đầy đủ 4 MB, dùng khi nạp lần đầu hoặc khôi phục qua USB/esptool tại địa chỉ `0x0`.

Firmware chỉ hỗ trợ ESP32; nhánh ESP8266 đã ngừng phát triển.

### Có gì mới ở firmware 1.3.16

- Giữ nguyên trạng thái Open/Closed khi nguồn tải 12 V hoặc box được cấp lại nguồn, miễn là nguồn không bị mất giữa lúc servo đang chạy. Cover đang Open sẽ không tự đóng.
- Nếu nguồn mất khi servo đang chạy, vị trí thực tế không còn chắc chắn nên firmware vẫn homing về đóng để an toàn.
- Giữ PWM servo liên tục khi cover đứng yên, loại bỏ hiện tượng servo giật khi nhả rồi gắn lại tín hiệu.
- Để tránh servo rè và nóng, cần đặt góc mở/đóng dừng trước điểm chặn cơ khí; không đặt góc servo sát hard-stop.
- Bao gồm tăng tốc cập nhật USB của 1.3.11: serial 115200 baud và gói dữ liệu 1024 byte.

## Lưu ý an toàn

- Không ngắt nguồn khi servo đang chạy hoặc khi firmware đang cập nhật.
- Không đặt góc mở hoặc đóng chạm điểm chặn cơ khí. Servo bị kẹt sẽ tiếp tục kéo, gây tiếng rè và nóng nhanh. Với thang 500–2500 µs tương ứng 0–270°, nên chừa ít nhất 5° trước điểm chặn; nếu điểm chặn thực tế là 267°, hãy bắt đầu thử ở khoảng 2450 µs (xấp xỉ 263°) rồi tinh chỉnh dần.
- Từ firmware 1.3.11, Serial Monitor hoặc công cụ USB Serial thủ công phải đặt tốc độ `115200 baud`. Website và ứng dụng Android không bị ảnh hưởng.
- Khi cập nhật, giữ Wi-Fi/USB ổn định đến khi Flat Panel tự khởi động lại.
- Main Cover và Scope Cover có cơ chế chặn để không chạy riêng lẻ cùng lúc.
