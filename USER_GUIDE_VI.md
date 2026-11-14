# Hướng dẫn sử dụng DIY Flat Panel

Tài liệu này dành cho người dùng cuối. DIY Flat Panel mặc định được điều khiển bằng **website tích hợp sẵn trong box**; không cần cài ứng dụng để sử dụng hằng ngày.

Phiên bản hiện tại: firmware `1.3.29`, ASCOM driver `1.0.19`, ứng dụng Android `2.6`. Các file tải xuống nằm tại [trang tải DIY Flat Panel](./README.md).

## 1. Chọn cách điều khiển

### Website — cách dùng mặc định

Website dùng được trên iPhone, iPad, Android, Windows, macOS, TV và mọi thiết bị có trình duyệt.

- Khi kết nối vào Wi-Fi của Flat Panel (AP mode), mở: `http://192.168.4.1`
- Khi Flat Panel đã kết nối Wi-Fi nhà (Station mode), mở: `http://flatpanel.local`

Website có điều khiển Main Cover, Scope Cover (nếu có), đèn Flat Panel, độ sáng, Auto Open, Auto Close, cấu hình servo, Wi-Fi Station và cập nhật firmware.

### Ứng dụng Android — tùy chọn

Ứng dụng Android dành cho người dùng muốn điều khiển bằng app thay vì website. Không bắt buộc phải cài.

### Driver ASCOM — dành cho N.I.N.A.

Driver ASCOM dành cho người dùng muốn điều khiển Main Cover và Flat Panel Light từ N.I.N.A. trên Windows.

## 2. Bắt đầu bằng website

1. Cấp nguồn cho DIY Flat Panel.
2. Trên điện thoại hoặc máy tính, kết nối Wi-Fi `FlatPanel_v1` nếu box chưa được cấu hình Wi-Fi nhà.
3. Mở `http://192.168.4.1`.
4. Trong tab **Configure**, nhập tên và mật khẩu Wi-Fi nhà **2,4 GHz**, bật Station rồi bấm **Save Wi-Fi and Connect**. Nút Save chỉ mở khi có cả tên và mật khẩu; tên chỉ gồm dấu cách không hợp lệ. Tên Wi-Fi có dấu cách vẫn được giữ nguyên. Khi tắt Station, có thể Save mà không cần nhập tên/mật khẩu.
5. Giữ kết nối với `FlatPanel_v1` và xem kết quả ngay dưới nút Save: đang kết nối, đã vào mạng nhưng chờ IP, thành công kèm IP hoặc thất bại kèm mã lỗi. **Đã lưu không đồng nghĩa đã kết nối.** Box không tự reboot hay chuyển trang khi lưu Wi-Fi trên web.
6. Khi thành công và có IP, web hiển thị đếm ngược **30 giây trước khi tắt `FlatPanel_v1`**. Chuyển điện thoại/máy tính sang cùng Wi-Fi nhà, rồi mở IP đã báo hoặc `http://flatpanel.local`. Nút **Open control page** chỉ hiện ở trang AP `192.168.4.1`; khi đã sang trang điều khiển qua Wi-Fi nhà thì tự ẩn và thông báo bạn đang ở trang điều khiển. Địa chỉ IP vẫn dùng được nếu thiết bị không phân giải được `flatpanel.local`.

Wi-Fi `FlatPanel_v1` được giữ trong lúc cấu hình hoặc kết nối thất bại; tự tắt 30 giây sau khi Station nhận được IP. Nếu Station mất kết nối, AP tự mở lại để chẩn đoán/cấu hình. Khi box chuyển kênh theo router, điện thoại có thể ngắt Wi-Fi ngắn; kết nối lại AP nếu còn phát. Mạng AP này không có mật khẩu: chỉ sử dụng ở môi trường tin cậy.

Nếu kết nối thất bại, chụp cả phần trạng thái và mã lỗi gửi người hỗ trợ; **không cần gửi mật khẩu**. Box chờ tối đa 30 giây mỗi lần thử, tự thử lại; sau nhiều lần thất bại sẽ chờ 5 phút trước chu kỳ tiếp theo. Có thể sửa thông tin rồi bấm Save để thử ngay. Lỗi xác thực/handshake không đủ khẳng định sai mật khẩu; còn có thể liên quan bảo mật router hoặc tín hiệu. Không nhận IP sau khi đã vào mạng thì cần kiểm tra DHCP của router.

Nếu box chỉ có Main Cover, tắt **Scope Cover installed** trong tab Configure. Thiết lập này được lưu trong box và Scope Cover sẽ được ẩn đi.

## 3. Dùng ứng dụng Android

1. Tải và cài file APK Android tại [trang tải](./README.md).
2. Lần cài đầu, Android có thể yêu cầu cho phép **Install unknown apps**.
3. Kết nối điện thoại với Flat Panel qua AP hoặc cùng Wi-Fi Station, rồi mở app và kết nối thiết bị.

## 4. Dùng với N.I.N.A.

1. Cài ASCOM Platform nếu máy chưa có.
2. Đóng N.I.N.A. và chạy file cài **DIY Flat Panel ASCOM Driver** tại [trang tải](./README.md).
3. Kết nối box với PC qua USB, mở N.I.N.A. và tại Flat Panel chọn **Viet DIY Flat Panel**.
4. Mở nút bánh răng / Setup, chọn **COM port** hoặc **Auto-detect DIY Flat Panel**, bấm **Save**, rồi Connect trong N.I.N.A.

Setup tự đọc cấu hình servo từ box và tự đọc lại khi đổi COM/Auto-detect. Nếu không đọc được box, vùng servo bị khóa nhưng vẫn có thể **Save** lựa chọn COM hoặc Auto-detect vào driver. **Save & Apply** chỉ gửi cấu hình servo đã thay đổi; không có thay đổi thì Save đóng cửa sổ như Cancel. Scope Cover là app/web-only và không được N.I.N.A. điều khiển.

Nếu đổi jack USB và Windows đổi số COM, chọn lại COM mới trong Setup hoặc bật Auto-detect. Nút Firmware Update cập nhật firmware trong box; để cập nhật driver trên PC, đóng N.I.N.A. rồi chạy file cài `.exe` mới.

## 5. Cập nhật firmware

Cách khuyến nghị là cập nhật từ website khi Flat Panel đang ở **Station mode**:

1. Mở `http://flatpanel.local`.
2. Vào **Configure** → **Firmware Update**.
3. Kiểm tra bản mới và xác nhận cập nhật.
4. Giữ nguyên nguồn và Wi-Fi cho tới khi box tự khởi động lại.

Driver ASCOM cũng có công cụ cập nhật qua cáp USB trong Setup → **Firmware Update**.

Từ driver **1.0.19**, giữ **Shift** khi bấm **Firmware Update...** để chọn firmware trên máy: bấm **Browse...**, chọn file `FlatPanel-...-ota.bin`, rồi **Install Local File**. Chế độ này không cần Internet và cho phép cài lại/hạ phiên bản. Chỉ dùng firmware DIY Flat Panel; không chọn `merged.bin` hay firmware DIY EAF. Bấm bình thường vẫn cập nhật online như trước.

Nếu đang dùng ASCOM driver 1.0.16 hoặc cũ hơn, cài driver mới tại [trang tải](./README.md) trước khi cập nhật firmware. Firmware từ 1.3.11 dùng Serial 115200 baud; driver 1.0.17 trở lên hỗ trợ tốc độ này.

### Nếu flash firmware thủ công, chọn đúng file firmware

- `FlatPanel-*-ota.bin`: chỉ dùng cho cập nhật OTA. Không flash file này tại địa chỉ `0x0`.
- `FlatPanel-*-merged.bin`: ảnh flash đầy đủ 4 MB, dùng khi nạp lần đầu hoặc khôi phục qua USB/esptool tại địa chỉ `0x0`.

## 6. Lưu ý khi sử dụng

- Không ngắt nguồn khi servo đang chạy hoặc khi firmware đang cập nhật.
- Không đặt góc mở hoặc đóng chạm điểm chặn cơ khí. Servo bị kẹt sẽ tiếp tục kéo, gây tiếng rè và nóng nhanh. Với thang 500–2500 µs tương ứng 0–270°, nên chừa ít nhất 5° trước điểm chặn; nếu điểm chặn thực tế là 267°, hãy bắt đầu thử ở khoảng 2450 µs (xấp xỉ 263°) rồi tinh chỉnh dần.
- Từ firmware 1.3.11, Serial Monitor hoặc công cụ USB Serial thủ công phải đặt tốc độ `115200 baud`. Website và ứng dụng Android không bị ảnh hưởng.
- Khi cập nhật, giữ nguồn và Wi-Fi/USB ổn định đến khi Flat Panel tự khởi động lại, rồi kết nối lại nếu cần.
- Điều khiển thủ công chỉ chạy từng cover; Auto Open/Auto Close có thể chạy hai cover cùng lúc nếu box đã bật Scope Cover.
- Từ 1.3.29, nếu MAC gốc của chip không hợp lệ (ví dụ toàn số 0), firmware tạo MAC thay thế riêng và lưu trong NVS trước khi bật Wi-Fi. Board có MAC gốc hợp lệ không bị thay đổi. Xem **Connection details → STA MAC**, nguồn `recovered-nvs` nghĩa là đang dùng MAC thay thế. Đây chỉ là giải pháp thử phục hồi địa chỉ mạng, không bảo đảm sửa được phần cứng Wi-Fi bị hỏng.
- MAC thay thế giữ nguyên qua tắt/bật nguồn và OTA sang các bản tiếp tục hỗ trợ cơ chế này. **Không xóa flash/NVS hoặc nạp lại merged image** nếu muốn giữ nguyên MAC thay thế; hãy cập nhật bằng OTA payload (qua Wi-Fi hoặc công cụ serial của driver). Hạ về firmware trước 1.3.29 sẽ không áp dụng MAC thay thế dù dữ liệu NVS còn. `esptool read-mac` vẫn đọc MAC gốc trong eFuse nên có thể tiếp tục hiện toàn số 0.
