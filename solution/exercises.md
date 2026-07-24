# K3 — Day 1: LLM API Exploration — Exercises

## Câu 1.1 — Độ nhạy của temperature

> Temperature 0.0 cho câu trả lời ổn định và thường lặp lại cách diễn đạt. Khi tăng đến 0.5, 1.0 và 1.5, chi tiết và từ ngữ đa dạng hơn. Temperature cao hữu ích cho ý tưởng sáng tạo nhưng tăng nguy cơ lan man hoặc thiếu chính xác.

## Câu 1.2 — Chọn temperature cho sản phẩm

> Tôi chọn khoảng 0.2–0.4 cho chatbot chăm sóc khách hàng. Mức này giúp câu trả lời nhất quán, bám chính sách và giảm bịa thông tin, nhưng vẫn không quá máy móc.

## Câu 1.3 — Đánh đổi chi phí

> GPT-4o có giá output 0.010 USD/1K token, GPT-4o-mini là 0.0006 USD/1K token, nên đắt hơn khoảng 16,7 lần. Workload là 10,5 triệu output token/ngày: 105 USD/ngày cho GPT-4o và 6,3 USD/ngày cho mini. GPT-4o phù hợp suy luận phức tạp; mini phù hợp FAQ và phân loại.

## Câu 2.1 — Sức mạnh của persona

> Persona giáo viên dùng câu ngắn, ví dụ gần gũi và tránh thuật ngữ. Persona chuyên gia tài chính dài hơn, dùng các khái niệm như sổ cái phân tán và đồng thuận. System prompt định hình độ chi tiết, giọng điệu và đối tượng người đọc. Nó là chỉ dẫn hành vi mạnh nhưng không bảo đảm tuyệt đối tính đúng đắn.

## Câu 2.2 — tiktoken vs đếm từ

> Với đoạn tiếng Việt khoảng 100 từ, `count_tokens` cho khoảng 150 token, còn số từ / 0,75 là 133 token; chênh lệch xấp xỉ 12,8%. Tokenizer BPE có thể tách chữ có dấu thành nhiều mảnh, nên tiếng Việt thường tốn nhiều token hơn tiếng Anh cùng độ dài. Tiktoken phù hợp hơn để dự toán chi phí.

## Câu 3.1 — Trải nghiệm người dùng với streaming

> Streaming quan trọng khi câu trả lời dài hoặc cần phản hồi ngay, vì người dùng có thể đọc khi model tiếp tục sinh. Nó đặc biệt phù hợp chat tương tác. Non-streaming hợp hơn khi cần kiểm tra, định dạng hoặc lưu toàn bộ kết quả trước khi hiển thị, chẳng hạn JSON hoặc tác vụ nền.

## Câu 3.2 — Vì sao backoff theo cấp số nhân?

> Exponential backoff giảm áp lực lên dịch vụ quá tải và cho dịch vụ thời gian hồi phục, trong khi vẫn thử lại lỗi thoáng qua. Nếu hàng nghìn client cùng retry sau 1 giây, chúng tạo “thundering herd” và làm lỗi kéo dài. Hệ thống thật nên thêm jitter để các lần retry phân tán hơn.

## Câu 4.1 — Thiết kế persona

> Persona: “Bạn là trợ giảng AI thân thiện. Trả lời bằng tiếng Việt, ngắn gọn, chính xác; giải thích từng bước khi người học yêu cầu và nêu rõ khi chưa chắc chắn.” “Bằng tiếng Việt” phù hợp học viên, còn “ngắn gọn, chính xác” giúp dễ đọc và hạn chế suy diễn.

## Câu 4.2 — Hạn chế và cải thiện

> Hạn chế lớn là assistant chỉ giữ ba lượt gần nhất nên mất ngữ cảnh dài hạn. Có thể tóm tắt hội thoại cũ khi history vượt ngưỡng, lưu summary rồi gửi system prompt + summary + ba lượt mới nhất vào API. Nên thêm kiểm tra an toàn trước khi hiển thị câu trả lời.
