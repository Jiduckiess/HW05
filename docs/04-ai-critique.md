# AI Critique

Trong bài này, AI giúp tôi chọn endpoint, tạo khung JMeter test plan, giải thích cách chạy JMeter và đọc file JTL. AI cũng giúp tôi phân biệt load, stress, spike và endurance test. Nhờ vậy tôi biết mỗi kịch bản cần số user, ramp-up, loop và timer khác nhau.

Điểm hữu ích nhất là AI trả lời nhanh khi tôi bị vướng ở JMeter, ví dụ chỗ thêm CSV Data Set Config, Response Assertion, Listener hoặc cách chạy bằng command line. AI cũng nhắc tôi chụp Activity Monitor để có evidence về CPU và RAM.

Tuy nhiên, tôi không dùng kết quả AI đưa ra ngay mà không kiểm tra. Các số trong report được đối chiếu lại với file JTL và màn hình JMeter. Ví dụ p95, max latency, số sample và throughput phải lấy từ kết quả chạy thật. AI không trực tiếp chạy test trên máy tôi nên không thể tự biết server có đang chạy hay không, cũng không thể thay tôi chụp evidence.

Một điểm cần chú ý là AI có thể đưa ra hướng dẫn chung nhưng chưa khớp hoàn toàn với SUT. Vì vậy tôi đã kiểm tra endpoint, request body, CSV và response code với project eShop trước khi chạy. Nếu có lỗi, tôi xem View Results Tree và log thay vì chỉ dựa vào AI.

Tóm lại, AI là công cụ hỗ trợ để hiểu bài và xử lý nhanh các bước kỹ thuật. Phần cấu hình, chạy test, kiểm tra kết quả và quyết định cuối cùng vẫn do tôi thực hiện và chịu trách nhiệm.

**Word count:** 270 (tính theo khoảng trắng, gồm tiêu đề và dòng đếm từ)
