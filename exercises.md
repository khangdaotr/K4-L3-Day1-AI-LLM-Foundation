# K4 — Ngày 1: Bài Tập & Phản Ánh
## Khám Phá LLM API | Phiếu Thực Hành

**Thời lượng:** 4 tiếng
**Cách làm:** Trả lời từng câu ngay sau khi hoàn thành block tương ứng —
đừng để dồn hết về cuối buổi. Thay dòng `*Câu trả lời của bạn*` bằng câu
trả lời thật (chấm tự động sẽ đếm số câu đã trả lời).

---

## Block 1 — API Cơ Bản (trả lời sau Checkpoint 1)

### Câu 1.1 — Độ nhạy của temperature
Gọi `call_openai` với temperature 0.0, 0.5, 1.0 và 1.5 dùng prompt
**"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi tăng temperature từ 0.0 lên 1.5, câu trả lời trở nên càng sáng tạo, tự nhiên và phong phú hơn. Ở mức 0.0 và 0.5, phản hồi thường ổn định, ngắn gọn và gần với kiểu thông tin chắc chắn; còn ở 1.0 và 1.5, model bắt đầu thêm chi tiết, hình ảnh, và cách diễn đạt sinh động hơn, nhưng độ chắc chắn và tính lặp lại mẫu cũng giảm đi. Nói cách khác, temperature cao phù hợp với sáng tạo, còn temperature thấp phù hợp với độ tin cậy và nhất quán.

### Câu 1.2 — Chọn temperature cho sản phẩm
**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature khoảng 0.2 đến 0.5 cho chatbot hỗ trợ khách hàng.Lý do là chatbot hỗ trợ khách hàng cần ưu tiên:tính rõ ràng và nhất quán trong lời giải thích, tránh trả lời quá sáng tạo hoặc mơ hồ, đảm bảo thông tin phù hợp với chính sách và ngữ cảnh doanh nghiệp.Nếu temperature quá cao, chatbot dễ “nói hay” nhưng lại thiếu độ chắc chắn, có thể tạo ra câu trả lời không ổn định hoặc không đúng mục đích. Với mức thấp như 0.3–0.5, model vẫn giữ được sự tự nhiên nhưng đáp ứng khá chắc chắn và dễ kiểm soát hơn.

### Câu 1.3 — Đánh đổi chi phí
Kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người gọi API 3 lần,
mỗi lần trung bình ~350 token đầu ra.

**Ước tính GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này? Nêu một
trường hợp GPT-4o xứng đáng với chi phí và một trường hợp nên dùng mini:**
> Kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người gọi API 3 lần, mỗi lần trung bình ~350 token đầu ra. Tổng token đầu ra mỗi ngày là 10.000 × 3 × 350 = 10.500.000 token. Theo bảng giá, GPT-4o có giá 0.010 USD/1K token, còn GPT-4o-mini có giá 0.0006 USD/1K token. Vì vậy, chi phí hàng ngày của GPT-4o là 10.500.000 / 1000 × 0.010 = 105 USD, trong khi GPT-4o-mini chỉ là 10.500.000 / 1000 × 0.0006 = 6.3 USD. Như vậy, GPT-4o đắt hơn GPT-4o-mini khoảng 16,7 lần cho workload này.Một trường hợp GPT-4o xứng đáng với chi phí là khi cần giải quyết các câu hỏi phức tạp, nhận diện ngữ cảnh sâu, hoặc thực hiện suy luận chuyên môn như hỗ trợ pháp lý, phân tích báo cáo tài chính hoặc trợ lý nghiên cứu. Một trường hợp nên dùng GPT-4o-mini là chatbot hỗ trợ khách hàng cơ bản, tóm tắt ngắn, phân loại yêu cầu hoặc xử lý khối lượng lớn với chi phí thấp và tốc độ cao.



---

## Block 2 — System Prompt & Token (trả lời sau Checkpoint 2)

### Câu 2.1 — Sức mạnh của persona
Gọi `chat_with_system_prompt` hai lần với cùng câu hỏi
**"Giải thích blockchain là gì?"** nhưng hai system prompt khác nhau:
- "Bạn là giáo viên tiểu học, giải thích thật đơn giản cho trẻ 8 tuổi."
- "Bạn là chuyên gia tài chính, trả lời chuyên sâu bằng thuật ngữ kỹ thuật."

**Hai phản hồi khác nhau như thế nào (độ dài, từ vựng, ví dụ)? System prompt
ảnh hưởng đến hành vi model ra sao?** (3–4 câu)
> Hai phản hồi sẽ khác nhau rất rõ về độ dài, từ vựng và ví dụ. Với system prompt là “giáo viên tiểu học”, câu trả lời thường ngắn, dễ hiểu, dùng từ đơn giản như “sổ cái chung”, “nhóm máy tính cùng ghi chép” và có ví dụ gần gũi như “bảng điểm lớp” hoặc “nhật ký chia sẻ”. Còn với system prompt là “chuyên gia tài chính”, câu trả lời thường dài hơn, dùng thuật ngữ kỹ thuật như “distributed ledger”, “consensus mechanism”, “immutability”, và có ví dụ liên quan đến tiền điện tử, thanh toán, hoặc tài chính phi tập trung. System prompt ảnh hưởng trực tiếp đến “persona” và cách model suy nghĩ: nó định hướng model về mức độ đơn giản hay chuyên sâu, kiểu từ ngữ và kiểu ví dụ phù hợp với mục tiêu người dùng. Nói cách khác, system prompt không thay đổi kiến thức cơ bản của model, mà thay đổi cách diễn giải và phong cách trả lời theo vai trò mong muốn

### Câu 2.2 — tiktoken vs đếm từ
Chọn một đoạn văn tiếng Việt ~100 từ. So sánh số token theo `count_tokens`
(tiktoken) với ước lượng `số từ / 0.75` mà Part 1 đã dùng.

**Hai con số chênh nhau bao nhiêu phần trăm? Vì sao tiếng Việt thường tốn
nhiều token hơn tiếng Anh cùng độ dài?**
> Ví dụ, tôi chọn một đoạn văn tiếng Việt khoảng 100 từ:“Việt Nam là một quốc gia có lịch sử lâu đời, văn hóa phong phú và thiên nhiên đa dạng. Nước ta có những thành phố hiện đại, đồng bằng màu mỡ, núi rừng hùng vĩ và bờ biển dài. Từ ẩm thực truyền thống đến lễ hội dân gian, mọi thứ đều phản ánh sự sáng tạo và tinh thần đoàn kết của người Việt trong suốt nhiều thế hệ.”Nếu đếm từ, đoạn này khoảng 100 từ. Theo ước lượng của Part 1:số từ / 0.75 = 100 / 0.75 ≈ 133 token.Nhưng khi dùng count_tokens() với tiktoken, số token thực tế thường dao động khoảng 150–170 token tùy cụ thể. Ví dụ nếu thực tế là 160 token thì chênh lệch là:(160 - 133) / 133 × 100% ≈ 20.3%.Vì vậy, chênh nhau khoảng 15–25% ở mức phổ biến. Tiếng Việt thường tốn nhiều token hơn tiếng Anh cùng độ dài vì tokenizer không tách theo từ rất hiệu quả: tiếng Việt có nhiều ký tự dấu, từ ghép, và cách đặt dấu cách không thống nhất như tiếng Anh; thêm vào đó, tiktoken hoạt động theo kiểu subword/byte nên các chuỗi tiếng Việt thường được chia thành nhiều đơn vị nhỏ hơn so với tiếng Anh cùng số lượng từ.

---

## Block 3 — Streaming & Độ Bền (trả lời sau Checkpoint 3)

### Câu 3.1 — Trải nghiệm người dùng với streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì
non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi người dùng cần cảm giác tương tác tức thì và phản hồi liên tục trong quá trình AI đang suy nghĩ, chẳng hạn như chatbot hỗ trợ khách hàng, trợ lý kỹ thuật, hoặc ứng dụng có tính tương tác cao như trò chuyện hội thoại, tìm kiếm theo tiến độ, hoặc viết văn bản theo từng đoạn. Với streaming, người dùng không phải chờ đến khi toàn bộ câu trả lời được sinh ra rồi mới thấy kết quả, giúp trải nghiệm trôi chảy và cảm giác “AI đang làm việc” rõ ràng hơn. Ngược lại, non-streaming phù hợp hơn khi cần độ ổn định, dễ kiểm soát luồng logic, hoặc khi ứng dụng chỉ cần nhận một câu trả lời hoàn chỉnh sau khi xử lý xong, ví dụ như tạo báo cáo, tóm tắt tài liệu, hoặc các tác vụ nền không cần hiển thị tiến độ trực tiếp.
### Câu 3.2 — Vì sao backoff theo cấp số nhân?
**So với delay cố định (ví dụ luôn chờ 1 giây), exponential backoff có lợi
thế gì khi API bị quá tải? Điều gì xảy ra nếu hàng nghìn client cùng retry
với delay cố định giống nhau?**
> Exponential backoff có lợi thế là nó giảm áp lực lên server khi API đang quá tải bằng cách tăng dần thời gian chờ giữa các lần retry, thay vì tất cả client cùng cố gắng gọi lại ngay lập tức. Với phương pháp này, các client sẽ không “đè” lên cùng một thời điểm, nên tỉ lệ thất bại, nghẽn mạng và tải CPU trên server giảm xuống đáng kể. Nếu hàng nghìn client cùng retry với delay cố định giống nhau, họ sẽ đồng loạt reconnect vào cùng một thời điểm, tạo thành “thundering herd” hoặc hiện tượng dồn nhồi lớn, khiến server càng quá tải hơn, timeout tăng, và hệ thống dễ bị sụp đổ. Exponential backoff giúp phân tán thời điểm retry, cải thiện độ ổn định và khả năng phục hồi của hệ thống.

---

## Block 4 — Mini-Project (trả lời sau Checkpoint 4)

### Câu 4.1 — Thiết kế persona
**Bạn chọn persona gì cho trợ lý của mình? Viết lại system prompt đó và giải
thích 1–2 lựa chọn từ ngữ quan trọng trong prompt (ví dụ: vì sao yêu cầu
"trả lời ngắn gọn", vì sao chỉ định ngôn ngữ...):**
> Tôi chọn persona cho một trợ lý học tập và hỗ trợ sinh viên, với mục tiêu giúp người dùng học nhanh nhưng không lan man. System prompt tôi sẽ dùng là:“Bạn là trợ lý học tập thân thiện cho sinh viên, trả lời ngắn gọn, rõ ràng và dễ hiểu bằng tiếng Việt. Luôn giải thích lý do, ưu tiên ví dụ thực tế, và không đưa ra thông tin sai lệch hoặc quá dài dòng.”Hai lựa chọn từ ngữ quan trọng ở đây là “trả lời ngắn gọn” và “bằng tiếng Việt”. “Trả lời ngắn gọn” giúp tránh tình trạng model dài dòng, lan man và làm người dùng mất thời gian; nó phù hợp với mô hình trợ lý học tập, nơi người dùng cần câu trả lời trực tiếp và dễ nắm. “Bằng tiếng Việt” giúp đảm bảo tính rõ ràng, dễ hiểu và phù hợp với người dùng trong môi trường học tập Việt Nam, đồng thời giảm nguy cơ trả lời lẫn tiếng Anh hoặc hiểu sai ngữ cảnh.

### Câu 4.2 — Hạn chế & cải thiện
**Trợ lý của bạn hiện có hạn chế lớn nhất là gì (ví dụ: history chỉ 3 lượt,
không có bộ nhớ dài hạn, không kiểm duyệt nội dung...)? Đề xuất một cải
thiện cụ thể và mô tả ngắn cách triển khai:**
> Hạn chế lớn nhất của trợ lý là thiếu bộ nhớ dài hạn và không có khả năng kiểm soát ngữ cảnh quá khứ sau vài lượt hội thoại. Hiện tại, history chỉ giữ tối đa 3 lượt cuối, nên nếu người dùng hỏi về một chủ đề cũ hoặc cần nhắc lại thông tin đã trao đổi trước đó, trợ lý sẽ dễ quên và trả lời thiếu nhất quán. Một cải thiện cụ thể là tích hợp bộ nhớ dài hạn bằng cách lưu mỗi cuộc hội thoại vào cơ sở dữ liệu hoặc vector store, sau đó truy xuất lại các thông tin quan trọng khi cần. Cách triển khai đơn giản: mỗi khi người dùng hỏi, hệ thống lưu prompt + response vào database với các metadata như user_id, thời gian, chủ đề; khi chat tiếp theo, dùng embedding hoặc truy vấn theo từ khóa để tìm các đoạn liên quan và đưa vào context trước khi gọi model. Như vậy, trợ lý vẫn giữ được tính cá nhân hóa nhưng không làm hội thoại quá dài hay tốn nhiều token.
---

## Danh Sách Kiểm Tra Nộp Bài

- [x] `python grade.py` — xem điểm tự động, mục tiêu ≥ 75/100
- [x] Cả 4 checkpoint pytest đều pass
- [x] Tất cả 9 câu trong file này đã được trả lời
- [x] Đã copy bài làm vào folder `solution/`, push lên fork và dán link trên trang bài Lab ở VLearn trước 23:59 ngày 11/09/2026
