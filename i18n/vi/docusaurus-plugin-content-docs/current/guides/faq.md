# Câu hỏi thường gặp (FAQs)

## Tại sao các từ gợi ý đều bằng tiếng Anh?

AiShort được tạo ra nhằm giúp người dùng không nói tiếng Anh dễ dàng hơn khi sử dụng ChatGPT.  
Tuy nhiên, tất cả các từ gợi ý hiện tại đều bằng tiếng Anh. Nguyên nhân là do ChatGPT hiểu tiếng Anh tốt hơn nhiều so với các ngôn ngữ khác.  
Ngay cả MOSS — mô hình hội thoại tiếng Trung quy mô lớn đầu tiên — cũng thừa nhận rằng các câu trả lời bằng tiếng Anh của nó vượt trội hơn.  
Vì vậy, khuyến nghị nên sử dụng gợi ý bằng tiếng Anh. (Hiện tại MOSS đã ngừng hoạt động)

Mặc dù việc sử dụng gợi ý bằng ngôn ngữ khác ngoài tiếng Anh vẫn có thể cho ra kết quả chấp nhận được, nhưng kết quả có thể thay đổi đáng kể nếu bạn nhập lại cùng một yêu cầu không phải tiếng Anh nhiều lần.  
Điều này là do ChatGPT hiểu các đầu vào không phải tiếng Anh theo cách khác nhau mỗi lần.  
Vì vậy, với các yêu cầu hướng đến năng suất, bạn nên dùng tiếng Anh để đảm bảo kết quả ổn định và đúng mong đợi.  

Ngoài ra, các câu trả lời được tạo ra từ yêu cầu tiếng Anh thường cũng sẽ bằng tiếng Anh.  
Bạn có thể buộc câu trả lời ở ngôn ngữ khác bằng cách thêm vào cuối yêu cầu, ví dụ: **“trả lời bằng tiếng Trung”**.  
Nếu tiếng mẹ đẻ của bạn là ngôn ngữ khác, hãy thay thế từ **“tiếng Trung”** bằng ngôn ngữ của bạn.

---

## Tôi có phải nhập lại yêu cầu mỗi lần không?

Trong API, bạn có thể đặt yêu cầu làm **“yêu cầu hệ thống”** để ChatGPT luôn tuân theo và bạn không cần nhập lại mỗi lần.  
Trong phiên bản web ChatGPT, nếu bạn chưa thay đổi yêu cầu chính, bạn chỉ cần đặt nội dung trả lời tiếp theo trong ngoặc kép, như vậy bạn không cần nhập lại yêu cầu.  
Nếu câu trả lời được tạo ra không đúng với yêu cầu ban đầu, điều đó có nghĩa là ChatGPT đã “quên” yêu cầu này. Trong trường hợp đó, bạn cần nhập lại để “căn chỉnh” lại hướng dẫn.  
Ngoài ra, mỗi liên kết hội thoại là duy nhất, bạn có thể lưu những hội thoại thường dùng vào **bookmark** để dễ truy cập và sử dụng sau này.


## Độ trễ khi tìm kiếm nhập liệu

Chức năng tìm kiếm được xây dựng dựa trên bản demo của Docusaurus và có một vấn đề liên quan đến việc tập trung phương thức nhập liệu trên giao diện PC.  
Sau khi mình báo lỗi này cho Docusaurus, họ trả lời rằng sẽ thử khắc phục, nhưng cho đến nay vẫn chưa có giải pháp.  
Họ còn để lại bình luận: *“FWIW, bạn không nên dùng tiếng Trung vì bản demo này không được bản địa hóa.”*  

Do đó, mình đã chia thành hai loại thành phần tìm kiếm: **di động** và **PC**.  
- Trên thiết bị di động: logic tìm kiếm giữ nguyên.  
- Trên PC (màn hình có độ rộng lớn hơn 768px): mình áp dụng hàm **“Debounce”** để xử lý vấn đề nhập liệu.  

Tuy nhiên, điều này dẫn đến hai hạn chế trên PC:  
1. Với đầu vào không phải tiếng Anh, bạn phải hoàn tất việc nhập trong vòng **800 mili giây**.  
2. Việc cập nhật tìm kiếm trên PC bị **trễ 800 mili giây**, thay vì hiển thị ngay lập tức.  

Nếu bạn có giải pháp tốt hơn, xin hãy phản hồi.

---

## Kết quả sai lệch thông tin

Mặc dù ChatGPT rất mạnh mẽ, nhưng không phải lúc nào cũng chính xác tuyệt đối.  
Đôi khi nó có thể xuất ra thông tin sai.  

Ví dụ: mình đã nhập hàng trăm thông tin vào AiShort và yêu cầu ChatGPT chuyển đổi dữ liệu sang một định dạng cụ thể. Trong quá trình đó, mình nhận thấy ChatGPT ghi sai một số chi tiết.  

Chẳng hạn, trong văn bản gốc có nhãn **“Filmkritiker”** (nhà phê bình phim), nhưng ChatGPT lại đổi thành **“Kinokritiker”**.  
Dù sự khác biệt này không ảnh hưởng nhiều trong ngữ cảnh văn bản, nhưng khi áp dụng trong mã nguồn thì sẽ gây lỗi.  

Vì vậy, khi sử dụng ChatGPT, bạn cần kiểm tra kỹ đầu ra.

---

## Các Prompt có kém hiệu quả không?

Nếu bạn đang thực hiện công việc **tóm tắt**, bạn có thể dùng GPT để tinh chỉnh và cải thiện câu trả lời ban đầu, giúp tăng độ chính xác.  

Ngoài ra, Prompt không chỉ hữu ích cho công việc sản xuất nội dung mà còn là công cụ kích thích tư duy.  
Nó giúp bạn mở rộng góc nhìn, tiếp cận câu hỏi theo nhiều hướng khác nhau, đồng thời nhận diện và xử lý những sai sót thường xuất hiện trong quá trình suy nghĩ.

Tất cả các Prompt được AiShort sử dụng đều thu thập từ Internet và thường xuyên được cập nhật trong **kho Prompt** của chúng tôi.  
Mặc dù mỗi Prompt đều đã được thử nghiệm kỹ, nhưng hiệu quả có thể khác nhau tùy theo nhu cầu cụ thể của từng người dùng.  

Nếu bạn gặp phải sự thiếu chính xác, có ý tưởng sáng tạo, hoặc phát hiện ra Prompt hữu ích, hãy cho chúng tôi biết qua mục [Phản hồi](/feedback), hoặc chia sẻ cùng cộng đồng của chúng tôi.
