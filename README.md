# WebRTC & Network Protocol Lab

Mô hình truyền nhận P2P real-time, phân tích SDP và so sánh TCP vs UDP, chạy hoàn toàn trong trình duyệt web. Không cần backend.

## Tính năng

- **Tab 1 — Kiến trúc & SDP Inspector.** Sơ đồ quy trình bắt tay Offer/Answer, kèm công cụ dán và phân bóc từng dòng SDP để xem rõ thông số tầng Transport và Application.
- **Tab 2 — P2P Chat Lab.** Kết nối DataChannel thật giữa hai peer qua copy-paste signal thủ công, đo RTT bằng ping/pong, so sánh kênh reliable (ordered) với unreliable (unordered, `maxRetransmits: 0`), và phát burst stream 10 gói/giây.
- **Tab 3 — Signaling tự động.** Giải thích cách thay copy-paste thủ công bằng Signaling Server (Socket.IO / WebSocket / Firebase) trong ứng dụng thực tế như Google Meet, Zoom, Zalo.

## Chạy local

WebRTC cần secure context nên phải qua HTTP server, mở trực tiếp file bằng `file://` sẽ không hoạt động.

Cách 1 — VS Code Live Server:

```
Mở thư mục này trong VS Code → chuột phải index.html → Open with Live Server
```

Cách 2 — dòng lệnh:

```bash
npx live-server --port=5500
```

Cách 3 — Python:

```bash
python -m http.server 5500
```

Sau đó vào `http://localhost:5500`.

### Thực hành trên 2 tab

1. Mở trang ở tab A và tab B.
2. Tab A: bấm **1. Tạo OFFER Signal**, chờ 2–3 giây cho trình duyệt quét ICE candidates rồi copy mã.
3. Tab B: dán vào ô **Nhập Signal Từ Đối Phương**, bấm **2. Chấp Nhận & Kết Nối**.
4. Copy mã ANSWER ở tab B, dán ngược lại tab A, bấm kết nối.

Bấm **🚀 Test Gửi Chuỗi Burst Stream** để thấy rõ khác biệt: kênh TCP-like giữ đủ thứ tự, kênh UDP-like có thể mất hoặc lộn xộn gói.

### Thực hành trên 2 máy

Cùng nối một mạng LAN rồi mở trang trên cả hai máy, gửi signal qua Zalo/Messenger/Email. Lưu ý: truy cập bằng địa chỉ IP LAN (`192.168.x.x`) sẽ bị trình duyệt chặn `getUserMedia`, cần HTTPS hoặc localhost.

## Cấu trúc

Toàn bộ nằm trong một file `index.html`: CSS và JavaScript inline, không phụ thuộc thư viện ngoài. STUN server dùng `stun:stun.l.google.com:19302`.

## Tài liệu tham khảo

- [WebRTC Crash Course](https://www.youtube.com/watch?v=FExZvpVvYxA&t=12s)
- [Cài WebServer trên VS Code](https://www.youtube.com/watch?v=E2sRb9kjHaM)
- [Giới thiệu WebRTC](https://www.youtube.com/watch?v=2Z2PDsqgJP8)
