# IoT-The-automatic-fish-tank
**Mô hình hệ thống hỗ trợ nuôi cá tự động có các tính năng sau:**
- Cho cá ăn và hẹn giờ cho cá ăn từ xa (chỉ cần có kết nối wifi có thể cho cá ăn từ bất kì đâu, khoảng cách nào)
- Kiểm tra nhiệt độ nước.
- Điều chỉnh ánh sáng.
- Màn hình LCD hiển thị thông tin.
- Kết nối mạng và IoT 





https://github.com/huedo2102/huedo2102/assets/118194834/e572c118-08b6-406e-8983-93ab9b4a7521





**Hệ thống phần cứng:**
- ESP8266 NodeMCU Lua V3 CH340
- Arduino Uno R3
- Đèn Led RGB 5050
- Động Cơ Servo SG90
- Biến trở chiết áp WH148 3 chân 1K
- Module thời gian thực DS3231 + ROM AT24C02
- Màn hình LCD 1602
- Cảm biến nhiệt độ DS18B20

![313404620-53ab29ee-49f0-405e-a9af-431d961b5eb8](https://github.com/huedo2102/huedo2102/assets/118194834/af4659b6-aef0-4773-8f6e-203114ce458e)


![313405105-6f92c0e0-d7a8-45c6-9230-9ee44bb14e59](https://github.com/huedo2102/huedo2102/assets/118194834/6c0a0f37-6c9b-4539-af90-d540172d5a87)


**Chức năng các khối:**
- Cảm biến: có nhiệm vụ đọc giá trị của các cảm biến đưa vào khối điều khiển. Linh kiện của khối này có cảm biến nhiệt độ DS18B20.
- Arduino là trung tâm điều khiển của hệ thống. Nó nhận dữ liệu từ khối cảm biến, xử lý dữ liệu đó và sau đó ra lệnh cho khối chấp hành điều khiển (như servo, led) để thực hiện các hành động cần thiết, như bật/tắt đèn, vv
- ESP8266 có chức năng truyền nhận tín hiệu từ IoT Cloud (Firebase) tới hệ thống. Kết nối hệ thống với Internet, cho phép giám sát và kiểm soát hệ thống từ xa thông qua ứng dụng di động. Nó cũng cho phép hệ thống gửi dữ liệu lên Firebase để lưu trữ và phân tích.
- Khối chấp hành điều khiển: Khối này chứa các thiết bị hành động như servo, Led. Dựa trên lệnh từ khối điều khiển, khối này thực hiện các hành động cụ thể, như bật/tắt đèn, vv..
  
**Kịch bản hoạt động:**

![313404645-fdc9ac9e-7c8f-441f-9c90-99904af6be42](https://github.com/huedo2102/huedo2102/assets/118194834/f48d9100-43fb-49f6-9962-a45093ca931b)


- Kết nối nguồn điện cho hệ thống, ESP8266 thực hiện việc kết nối Internet cho hệ thống, Arduino hoạt động thực hiện việc điều khiển các thiết bị: servo cho cá ăn, độ sáng đèn led, hiển thị nhiệt độ nước và thời gian thực lên màn hình LCD và ứng dụng trên điện thoại di động.
- Cho ăn bán tự động: người dùng chưa thiết lập lịch cho ăn, người dùng sẽ ấn nút cho cá ăn trên ứng dụng, tín hiệu truyền đến Firebase sau đó sẽ được ESP8266 lấy xuống và truyền cho Arduino thực hiện việc quay servo. Servo quay, nắp hộp thức ăn mở trong vài giây, sau đó servo sẽ quay lại để đóng nắp hộp.
- Cho ăn tự động: người dùng thiết lập lịch cho ăn, khi đến lịch ứng dụng tự động gửi tín hiệu đến Firebase sau đó sẽ được ESP8266 lấy xuống và truyền cho Arduino thực hiện việc quay servo. Servo quay, nắp hộp thức ăn mở trong vài giây, sau đó servo sẽ quay lại để đóng nắp hộp. Hệ thống sẽ tiếp tục hoạt động và lặp lại quá trình theo thời gian được đặt ra hoặc cho đến khi hệ thống bị ngắt kết nối Internet hoặc tắt nguồn.
- Điều chỉnh đèn led: tùy vào nhu cầu ánh sáng, người dùng sẽ điều chỉnh đèn led qua ứng dụng, sau đó ứng dụng sẽ truyền tín hiệu đến Firebase. ESP8266 sẽ lấy tín hiệu từ Firebase xuống và truyền cho Arduino thực hiện điều chỉnh đèn.
- Lấy thời gian thực: thời gian thực sẽ được lấy dựa trên ứng dụng cập nhật theo thiết bị di động, ứng dụng cập nhật thời gian lên Firebase, ESP8266 kết nối Internet và lấy dữ liệu thời gian thực từ Firebase truyền đến Arduino để hiển thị lên LCD.
- Kiểm tra nhiệt độ: cảm biến nhiệt độ sẽ cảm ứng nhiệt độ nước truyền tín hiệu qua Arduino, Arduino truyền tín hiệu qua ESP8266 đến Firebase và cập nhật lên ứng dụng.


![313404671-c61d40fc-267a-4336-b635-ee8394f86085](https://github.com/huedo2102/huedo2102/assets/118194834/014b09ed-4c15-43cd-a270-936649b3ad73)


**Hình ảnh hệ thống:**


![313404679-3e58b847-d270-400f-9eac-abb162baa43e](https://github.com/huedo2102/huedo2102/assets/118194834/df44ce0e-d213-4561-a364-681b0a8ec655)


**Giao diện ứng dụng điều khiển trên Smart phone:**

![313404695-d1ae3d32-a503-415b-bdb0-e7d16cc791ac](https://github.com/huedo2102/huedo2102/assets/118194834/a44462c0-9498-40f9-96dc-469106bff3cb)


**Firebase:**

![313404703-fce30506-22d8-4857-8cb6-7b3c354646e2](https://github.com/huedo2102/huedo2102/assets/118194834/708ef2a5-6e45-48b7-bb3a-1b7a3062f92a)


