**BÀI LÀM: KỸ THUẬT RAG GROUNDING DẬP TẮT ẢO GIÁC HỢP ĐỒNG THU MUA**

**Phần 1: Phân tích nguyên nhân ảo giác (Hallucination)**
AI đưa ra con số sai lệch (phạt 20% và đình chỉ 30 ngày) nhưng lại cực kỳ tự tin vì người dùng đã mắc lỗi **hỏi LLM không kèm tài liệu nguồn (Context/Grounding)**. Khi thiếu dữ liệu tham chiếu nội bộ (quy định riêng của MartX), mô hình ngôn ngữ sẽ tự động suy đoán dựa trên trọng số xác suất và các dữ liệu chung chung trên Internet để tạo ra một câu trả lời nghe có vẻ hợp lý và trôi chảy. Nó chắp vá các mức phạt phổ biến của các hợp đồng khác để điền vào chỗ trống thay vì phản hồi là "không biết", dẫn đến hiện tượng Ảo giác (Hallucination).

**Phần 2: Cấu trúc RAG Prompt hoàn chỉnh**
Để khắc phục hoàn toàn tình trạng ảo giác, cần cung cấp cho AI một Prompt sử dụng kỹ thuật RAG Grounding như sau:

> **[1. Văn bản hợp đồng chuẩn - CONTEXT]**
> Trích đoạn hợp đồng thu mua MartX: "Phạt 5% giá trị lô bị dập nát và yêu cầu đổi hàng trong 24h."
> 
> **[2. Câu hỏi nghiệp vụ - USER QUERY]**
> Dựa vào tài liệu trên, hãy cho biết: Theo quy định MartX, nhà cung cấp giao rau bị dập nát trên 10% thì bị phạt bao nhiêu?
> 
> **[3. Khóa an toàn - NEGATIVE CONSTRAINT]**
> Nếu thông tin không có trong văn bản, tuyệt đối trả lời 'Không có dữ liệu trong tài liệu', không tự suy đoán.
