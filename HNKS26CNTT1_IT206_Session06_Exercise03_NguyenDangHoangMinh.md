# Báo cáo so sánh hai cách viết prompt gia sư Feynman và chấm bài theo rubric

## Bước 1. Đề xuất hai prompt mẫu

Hai phương án cùng giải quyết một bài toán: sinh viên giải thích một khái niệm bằng lời của mình, AI chấm phần giải thích và đặt câu hỏi giúp sinh viên tự phát hiện chỗ hiểu sai.

### Giải pháp 1 — Prompt đơn giản

> Hãy làm gia sư theo phương pháp Feynman. Đọc bài giải thích của sinh viên về [CHỦ_ĐỀ], chấm trên thang 10 theo ba tiêu chí: chính xác, dễ hiểu và có ví dụ. Nhận xét ngắn gọn và đặt một câu hỏi để sinh viên tự cải thiện bài.
>
> Bài giải thích: [BÀI_LÀM]

### Giải pháp 2 — Prompt chi tiết

> Bạn là gia sư cho sinh viên năm nhất ngành Công nghệ thông tin. Hãy dùng phương pháp Feynman để giúp sinh viên giải thích [CHỦ_ĐỀ] bằng lời của mình.
>
> 1. Nếu [BÀI_LÀM] trống, hãy yêu cầu sinh viên tự giải thích chủ đề trong 2–3 câu rồi dừng và chờ câu trả lời.
> 2. Khi có bài làm, hãy chấm theo rubric dưới đây. Chỉ đánh giá những gì sinh viên đã viết.
>    - **Chính xác (0–4 điểm):** 4 nếu đúng các ý cốt lõi, 2 nếu có ý đúng nhưng còn một lỗi kiến thức quan trọng, 0 nếu sai ý chính hoặc lạc đề.
>    - **Dễ hiểu (0–3 điểm):** 3 nếu người mới học có thể hiểu ngay, 1 nếu có thuật ngữ khó mà chưa giải thích, 0 nếu không xác định được ý muốn nói.
>    - **Ví dụ (0–3 điểm):** 3 nếu có tình huống cụ thể minh họa đúng, 1 nếu có ví dụ liên quan nhưng chưa làm rõ khái niệm, 0 nếu thiếu ví dụ hoặc ví dụ sai.
> 3. Trình bày bảng gồm ba cột: Tiêu chí, Điểm, Căn cứ từ bài làm. Cộng điểm của ba tiêu chí và ghi tổng trên 10.
> 4. Kết thúc bằng đúng một câu hỏi gợi mở về điểm cần cải thiện nhất. Đợi sinh viên sửa bài rồi chấm lại bằng cùng rubric.
>
> Bài giải thích của sinh viên: [BÀI_LÀM]

## Bước 2. Bảng so sánh trade-off

| Tiêu chí | Giải pháp 1 (đơn giản) | Giải pháp 2 (chi tiết) |
|---|---|---|
| Độ dễ hiểu | Cao. Prompt ngắn, sinh viên có thể dùng ngay. | Trung bình. Người dùng cần đọc cả quy trình và các mức điểm. |
| Chi phí token | Ít. Phù hợp khi cần góp ý nhanh cho một bài. | Nhiều hơn do phải gửi rubric và xuất bảng chấm. |
| Tính nhất quán khi chấm | Thấp hơn. AI tự quyết định mỗi tiêu chí chiếm bao nhiêu điểm. | Cao hơn. Các bài đều dùng cùng trọng số 4–3–3 và cùng mô tả mức điểm. |
| Khả năng xử lý trường hợp biên | Trung bình. Prompt chưa quy định cách xử lý bài trống hoặc thiếu ví dụ. | Tốt với các trường hợp đã quy định. Bài trống thì hỏi lại, thiếu ví dụ thì tiêu chí đó nhận 0 điểm. |
| Tính linh hoạt | Cao. Dễ đổi chủ đề hoặc dùng trong một lượt hỏi đáp. | Cần chỉnh rubric nếu chuyển sang bài có yêu cầu khác, chẳng hạn bài chứng minh toán học. |

## Bước 3. Lựa chọn và chạy thử

**Chọn Giải pháp 2.** Bài toán cần vừa hướng dẫn sinh viên tự sửa vừa chấm nhiều lần. Rubric cố định giúp sinh viên biết chính xác mình mất điểm ở đâu và đối chiếu được kết quả trước và sau khi sửa. Với mục tiêu này, chi phí token bổ sung là hợp lý.

### Dữ liệu chạy thử

- **[CHỦ_ĐỀ]**: Vai trò của RAM.
- **[BÀI_LÀM]**: “RAM là bộ nhớ tạm, chứa dữ liệu mà máy tính đang sử dụng. Khi tắt máy, dữ liệu trong RAM vẫn còn nguyên.”

### Kết quả lượt 1

| Tiêu chí | Điểm | Căn cứ từ bài làm |
|---|---|---|
| Chính xác | 2/4 | Ý “chứa dữ liệu mà máy tính đang sử dụng” đúng. Ý “khi tắt máy, dữ liệu trong RAM vẫn còn nguyên” sai đối với RAM thông thường. |
| Dễ hiểu | 3/3 | Hai câu ngắn, dùng từ quen thuộc và diễn đạt rõ điều sinh viên muốn nói. |
| Ví dụ | 0/3 | Bài chưa đưa ra tình huống sử dụng RAM cụ thể. |

**Tổng điểm: 5/10.**

**Câu hỏi gợi mở:** Khi em đang gõ văn bản, nếu máy mất điện trước khi em lưu và phần mềm chưa tự động lưu, điều gì sẽ xảy ra với phần vừa gõ?

### Bài sửa của sinh viên

> RAM giữ tạm dữ liệu mà máy tính đang dùng. Ví dụ, khi em gõ văn bản, phần vừa gõ được giữ trong RAM. Nếu máy mất điện trước khi em hoặc phần mềm kịp lưu, phần đó sẽ mất.

### Kết quả lượt 2

| Tiêu chí | Điểm | Căn cứ từ bài sửa |
|---|---|---|
| Chính xác | 4/4 | Bài nêu đúng vai trò lưu tạm và giải thích đúng điều xảy ra với dữ liệu chưa lưu khi mất điện. |
| Dễ hiểu | 3/3 | Cách nói “phần vừa gõ” giúp người mới học hình dung được dữ liệu đang dùng. |
| Ví dụ | 3/3 | Tình huống soạn văn bản minh họa trực tiếp vai trò của RAM. |

**Tổng điểm: 10/10.**

**Câu hỏi gợi mở:** Nếu em đã lưu văn bản vào ổ SSD trước khi mất điện, vì sao em vẫn mở lại được tệp sau khi bật máy?
