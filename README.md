# DIY Flat Panel Downloads (ESP32)

Kho phát hành này chỉ chứa các file cần thiết cho người dùng DIY Flat Panel. Source code được quản lý riêng và không được upload vào repository này.

## Tải xuống

- [Firmware ESP32 1.0.1 - OTA payload](./FlatPanel-1.0.1-ota.bin)
- [Firmware ESP32 1.0.1 - ảnh flash đầy đủ 4 MB](./FlatPanel-1.0.1-merged.bin)
- [Ứng dụng Android 1.3](./DIY-Flat-Panel-Android-1.3.apk)

## Chọn đúng file firmware

- File `*-ota.bin` là application binary dùng cho chức năng **Firmware Update over Wi-Fi** trong ứng dụng Android. Không flash file này tại địa chỉ `0x0`.
- File `*-merged.bin` là ảnh flash đầy đủ 4 MB, dùng để nạp lần đầu hoặc khôi phục thiết bị bằng esptool tại địa chỉ `0x0`.
- Firmware chỉ hỗ trợ ESP32. Nhánh ESP8266 đã ngừng phát triển và không được phát hành tại đây.

## Cập nhật qua Wi-Fi

1. Kết nối ứng dụng Android với Flat Panel qua Wi-Fi AP hoặc Wi-Fi Station.
2. Mở tab **Configure** và chọn **Check for Firmware Update**.
3. Giữ nguồn và kết nối Wi-Fi ổn định cho đến khi thiết bị tự khởi động lại.

Ứng dụng kiểm tra model, phiên bản protocol, kích thước, CRC32 và SHA-256 trước khi truyền firmware. ESP32 kiểm tra lại kích thước, thứ tự chunk và CRC32 trước khi chuyển sang phân vùng OTA mới.

Firmware `1.0.1` tăng kích thước chunk OTA qua Wi-Fi từ 64 lên 1024 byte và không ghi nội dung chunk HEX ra Serial, giúp giảm mạnh số lượt gửi/ACK và thời gian cập nhật. Ứng dụng vẫn tự động dùng chunk 64 byte khi kết nối firmware cũ.

Lần nâng cấp từ firmware `1.0.0` lên `1.0.1` vẫn phải dùng giới hạn 64 byte do firmware đang chạy quyết định kích thước chunk. Có thể chờ lần OTA này hoàn tất, hoặc flash file `1.0.1-merged.bin` qua USB để chuyển nhanh. Từ firmware `1.0.1` trở đi, OTA Wi-Fi sẽ dùng chunk 1024 byte.

## File manifest

`update-manifest.json` được ứng dụng Android đọc trực tiếp từ:

`https://raw.githubusercontent.com/VietNM127/FlatPanel_Downloads/main/update-manifest.json`
