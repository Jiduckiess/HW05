# AI Critique

AI giúp tôi chọn endpoint, tạo JMeter test plan, giải thích cách chạy và đọc file JTL. AI cũng nhắc tôi chụp Activity Monitor để có evidence về CPU và RAM.

Điểm AI đưa ra chưa đúng là kết luận từ ba run ngắn rằng đã tìm được threshold của máy. Kết luận này thiếu vì Load, Stress và Spike chỉ chạy trong thời gian ngắn; Spike còn không có giai đoạn recovery. Sau đó tôi chạy endurance gần 15 phút và kiểm tra raw JTL. Kết quả chỉ cho thấy hệ thống ổn định ở 10 users, ít nhất 9.66 samples/giây, p95 3 ms và không có lỗi. Nó không chứng minh đây là throughput tối đa của máy M4 Pro hay của SUT.

Lý do AI dễ đưa ra kết luận quá rộng là AI chỉ dựa vào số liệu được gửi. AI không trực tiếp quan sát máy tôi, cũng không tự kiểm tra cấu hình JMeter hoặc source code SUT. Vì vậy các số p95, max latency, số sample và throughput phải được đối chiếu với raw JTL, không chỉ nhìn Aggregate hoặc Summary Report.

Tôi cũng kiểm tra lại endpoint, request body, CSV, token JWT và response code với project eShop trước khi chạy. Khi có nghi ngờ, tôi xem View Results Tree và log thay vì tin ngay vào AI. Qua bài này, tôi hiểu AI hữu ích để gợi ý và giải thích nhanh, nhưng phần chạy test, kiểm tra evidence và kết luận cuối cùng vẫn là trách nhiệm của tôi.

**Word count:** 280 (tính theo khoảng trắng, gồm tiêu đề và dòng đếm từ)
