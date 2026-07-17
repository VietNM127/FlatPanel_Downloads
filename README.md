# DIY Flat Panel Downloads (ESP32)

Kho phát hành này chỉ chứa các file cần thiết cho người dùng DIY Flat Panel. Source code được quản lý riêng và không được upload vào repository này.

## Tải xuống

- [Firmware ESP32 1.0.2 - OTA payload](./FlatPanel-1.0.2-ota.bin)
- [Firmware ESP32 1.0.2 - ảnh flash đầy đủ 4 MB](./FlatPanel-1.0.2-merged.bin)
- [Ứng dụng Android 2.0](./DIY-Flat-Panel-Android-2.0.apk)

## Chọn đúng file firmware

- File `*-ota.bin` là application binary dùng cho chức năng **Firmware Update over Wi-Fi** trong ứng dụng Android. Không flash file này tại địa chỉ `0x0`.
- File `*-merged.bin` là ảnh flash đầy đủ 4 MB, dùng để nạp lần đầu hoặc khôi phục thiết bị bằng esptool tại địa chỉ `0x0`.
- Firmware chỉ hỗ trợ ESP32. Nhánh ESP8266 đã ngừng phát triển và không được phát hành tại đây.

## Cập nhật qua Wi-Fi

1. Kết nối ứng dụng Android với Flat Panel qua Wi-Fi Station.
2. Mở tab **Configure** và chọn **Check for Firmware Update**.
3. Giữ nguồn và kết nối Wi-Fi ổn định cho đến khi thiết bị tự khởi động lại.

Ứng dụng kiểm tra model, phiên bản protocol, kích thước, CRC32 và SHA-256 trước khi truyền firmware. ESP32 kiểm tra lại kích thước, thứ tự chunk và CRC32 trước khi chuyển sang phân vùng OTA mới.

Firmware `1.0.1` tăng kích thước chunk OTA qua Wi-Fi từ 64 lên 1024 byte và không ghi nội dung chunk HEX ra Serial, giúp giảm mạnh số lượt gửi/ACK và thời gian cập nhật. Ứng dụng vẫn tự động dùng chunk 64 byte khi kết nối firmware cũ.

Lần nâng cấp từ firmware `1.0.0` lên `1.0.1` vẫn phải dùng giới hạn 64 byte do firmware đang chạy quyết định kích thước chunk. Có thể chờ lần OTA này hoàn tất, hoặc flash file `1.0.1-merged.bin` qua USB để chuyển nhanh. Từ firmware `1.0.1` trở đi, OTA Wi-Fi sẽ dùng chunk 1024 byte.

Firmware `1.0.2` cải thiện Station reconnect: thay thế TCP client cũ bị treo, chủ động reconnect khi mất Wi-Fi và khởi động lại TCP/UDP/mDNS sau khi đường truyền phục hồi. Android `1.4` tìm thiết bị lần lượt bằng IP Station đã lưu, mDNS và UDP broadcast nhiều lần; đồng thời ngăn các thread reconnect cũ phá kết nối mới.

Android `1.5` thêm cache-buster khi kiểm tra `update-manifest.json`, tránh nhận manifest cũ từ cache GitHub/CDN ngay sau khi phát hành bản mới.

Android `1.6` chỉ bật cập nhật khi phiên bản firmware công bố mới hơn firmware đang chạy. Phiên bản bằng hoặc thấp hơn sẽ hiển thị `No Update` và không cho cài lại.

Android `1.7` hiển thị trạng thái firmware đã mới nhất bằng màu xanh lá để người dùng nhận biết nhanh.

Android `1.8` chỉ cho kiểm tra và cập nhật firmware khi thiết bị đang kết nối qua Wi-Fi Station. Ở AP mode, nút cập nhật đổi thành `Station mode only` và bị vô hiệu hóa vì điện thoại không có đường Internet phù hợp để tải firmware.

Android `1.9` khắc phục lỗi APK `1.8` bị thiếu class Kotlin `MainActivity$Companion` và thoát ngay khi mở. Quy trình phát hành từ bản này luôn clean build toàn bộ DEX; trạng thái nút OTA cũng chỉ được cập nhật theo session Wi-Fi thực tế.

Android `2.0` chuyển sang release keystore cố định và bổ sung cập nhật ứng dụng ngay trong app. Khi có phiên bản mới hơn, app tải APK từ kho phát hành, kiểm tra kích thước và SHA-256 rồi mở trình cài đặt Android để người dùng xác nhận.

## Cập nhật ứng dụng Android

App tự kiểm tra phiên bản Android mới khi khởi động và chỉ hiển thị hộp thoại nếu manifest công bố phiên bản cao hơn bản đang cài. Lần đầu sử dụng, Android/FydeOS có thể yêu cầu cấp quyền **Install unknown apps**; hệ điều hành luôn yêu cầu người dùng xác nhận trước khi cài.

Android `2.0` là bản đầu tiên dùng release key cố định. Nếu thiết bị đang cài bản `1.9` trở xuống được ký bằng debug key cũ, cần gỡ bản cũ và cài `2.0` một lần. Từ các bản sau có thể cập nhật trực tiếp trong app.

## File manifest

`update-manifest.json` được ứng dụng Android đọc trực tiếp từ:

`https://raw.githubusercontent.com/VietNM127/FlatPanel_Downloads/main/update-manifest.json`
