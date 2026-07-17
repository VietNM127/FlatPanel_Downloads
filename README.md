# DIY Flat Panel Downloads (ESP32)

Kho phát hành này chỉ chứa các file cần thiết cho người dùng DIY Flat Panel. Source code được quản lý riêng và không được upload vào repository này.

## Tải xuống

- [Firmware ESP32 1.0.0 - OTA payload](./FlatPanel-1.0.0-ota.bin)
- [Firmware ESP32 1.0.0 - ảnh flash đầy đủ 4 MB](./FlatPanel-1.0.0-merged.bin)
- [Ứng dụng Android 1.2](./DIY-Flat-Panel-Android-1.2.apk)

## Chọn đúng file firmware

- File `*-ota.bin` là application binary dùng cho chức năng **Firmware Update over Wi-Fi** trong ứng dụng Android. Không flash file này tại địa chỉ `0x0`.
- File `*-merged.bin` là ảnh flash đầy đủ 4 MB, dùng để nạp lần đầu hoặc khôi phục thiết bị bằng esptool tại địa chỉ `0x0`.
- Firmware chỉ hỗ trợ ESP32. Nhánh ESP8266 đã ngừng phát triển và không được phát hành tại đây.

## Cập nhật qua Wi-Fi

1. Kết nối ứng dụng Android với Flat Panel qua Wi-Fi AP hoặc Wi-Fi Station.
2. Mở tab **Configure** và chọn **Check for Firmware Update**.
3. Giữ nguồn và kết nối Wi-Fi ổn định cho đến khi thiết bị tự khởi động lại.

Ứng dụng kiểm tra model, phiên bản protocol, kích thước, CRC32 và SHA-256 trước khi truyền firmware. ESP32 kiểm tra lại kích thước, thứ tự chunk và CRC32 trước khi chuyển sang phân vùng OTA mới.

## File manifest

`update-manifest.json` được ứng dụng Android đọc trực tiếp từ:

`https://raw.githubusercontent.com/VietNM127/FlatPanel_Downloads/main/update-manifest.json`
