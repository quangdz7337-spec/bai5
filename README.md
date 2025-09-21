# bai5
# Điều khiển LED qua UART (USART1) với STM32
- Cấu hình UART trên STM32F1.
- Viết chương trình gửi chuỗi ""Hello from STM32!"" tới máy tính. 
- Sử dụng phần mềm terminal để hiển thị chuỗi này.
- Khi gửi một ký tự từ máy tính, STM32 sẽ phản hồi lại ký tự đó.
- Khi gửi chuỗi ""ON"" thì bật đèn, ""OFF"" thì tắt đèn."

---

## Tính năng
- Cấu hình **USART1 (TX: PA9, RX: PA10)** với baudrate **9600**.
- Nhận dữ liệu từ terminal UART.
- Phản hồi (echo) lại ký tự vừa nhận.
- Nhận và xử lý 2 lệnh chính:
  - `ON` → Bật LED (PA0 = LOW).
  - `OFF` → Tắt LED (PA0 = HIGH).
- Gửi thông báo trạng thái về terminal.

---

## Kết nối phần cứng
- STM32F103C8T6 (Blue Pill).
- Bộ chuyển USB-to-UART:
  - **PA9 (TX)** → RX của USB-UART.
  - **PA10 (RX)** → TX của USB-UART.
  - **GND** → GND chung.
- LED nối vào **PA0** (trên một số board có sẵn LED này).

---

## Cách sử dụng
1. Nạp chương trình vào STM32.
2. Mở phần mềm terminal (VD: PuTTY, Tera Term, Arduino Serial Monitor).
3. Cấu hình cổng COM với tốc độ **9600, 8N1** (8 data bits, No parity, 1 stop bit).
4. Gõ lệnh:
   - `ON` + Enter → LED bật.
   - `OFF` + Enter → LED tắt.
5. Terminal sẽ hiện phản hồi từ board.

---

## Mô tả code
- **UART1_Config()** → Cấu hình USART1 và tốc độ baud.
- **GPIO_Config()** → Cấu hình PA0 làm ngõ ra điều khiển LED.
- **UART1_SendChar() / UART1_SendStr()** → Gửi dữ liệu UART.
- **UART1_GetChar()** → Nhận ký tự UART.
- **main()**:
  - Khởi tạo GPIO và UART.
  - Nhận lệnh từ UART.
  - So sánh chuỗi `"ON"` hoặc `"OFF"` để bật/tắt LED.

---

## Ví dụ kết quả
```text
Hello from STM32!
ON
LED ON
OFF
LED OFF
