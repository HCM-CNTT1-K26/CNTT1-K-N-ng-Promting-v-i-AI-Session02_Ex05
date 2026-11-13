### Phần 1: Cơ chế hoạt động của In-Context Learning (ICL)

* **Cách AI học không cần train lại model:** Khác với việc fine-tune (phải chạy lại dữ liệu để cập nhật trọng số bên trong mạng neural), In-Context Learning cho phép AI học ngay lúc suy luận (Inference). Khi ta kẹp các ví dụ mẫu trực tiếp vào Prompt, cơ chế Self-Attention sẽ tự đối chiếu và tìm ra quy luật tương ứng giữa Input và Output ngay trong phiên chat đó, từ đó điều chỉnh câu trả lời cho khớp mà không làm thay đổi lõi mô hình gốc.
* **Lý do Few-shot vượt trội hơn Zero-shot khi gặp câu mỉa mai:**
* Với **Zero-shot**, AI chỉ bắt mặt chữ theo nghĩa đen (Surface Lexical Meaning). Thấy từ *"đẹp mê ly"*, *"khỏi cần bật lò sưởi"*, máy tự mặc định là khen vì không hiểu ngữ cảnh kỹ thuật CPU 98°C là quá nóng.
* Khi đưa **Few-shot** vào, các ví dụ mẫu đóng vai trò định hướng ngữ cảnh giúp AI hiểu cách nói chuyện của dân công nghệ: cứ hễ câu khen đi kèm với thông số bất thường (nhiệt độ cao, pin hẻo, ship lâu) thì đó là khen đểu và phải xếp vào **TIÊU CỰC**.



---

### Phần 2: Prompt Few-shot xử lý đánh giá mỉa mai tại TechShop


Phân loại cảm xúc đánh giá sản phẩm tại TechShop thành 2 nhãn: [TÍCH CỰC] hoặc [TIÊU CỰC] kèm lý do ngắn gọn. Lưu ý: khách công nghệ hay dùng cách nói mỉa mai, khen ngược để chê lỗi phần cứng và dịch vụ.

Ví dụ 1 (Về nhiệt độ):
Input: "Laptop vỏ nhôm sang xịn, mỗi tội render một lúc là mặt phím đủ nóng để chiên trứng luôn."
Output: TIÊU CỰC | Lý do: Mỉa mai máy tản nhiệt kém, quá nóng khi chạy nặng.

Ví dụ 2 (Về pin):
Input: "Máy sạc nhanh lắm, pin thì rèn tính kiên nhẫn cực tốt vì cứ 2 tiếng lại được cắm sạc một lần."
Output: TIÊU CỰC | Lý do: Chê pin tụt nhanh (2 tiếng hết pin) bằng giọng châm biếm.

Ví dụ 3 (Về giao hàng):
Input: "Shop giao hàng tốc độ ánh sáng, đặt từ lúc mới lĩnh lương mà tới lúc hết tiền mới nhận được hàng."
Output: TIÊU CỰC | Lý do: Nói ngược để chê giao hàng quá chậm.

Cần phân loại:
Input: "Máy thiết kế đẹp mê ly, cầm rất đầm tay, mùa đông ôm máy chơi game thì khỏi cần bật lò sưởi vì nhiệt độ CPU lên hẳn 98 độ C!"
Output:



**Kết quả AI trả về:**

TIÊU CỰC | Lý do: Khen thiết kế nhưng thực chất đang mỉa mai lỗi máy quá nóng (CPU lên tới 98 độ C) qua câu nói "khỏi cần bật lò sưởi".
