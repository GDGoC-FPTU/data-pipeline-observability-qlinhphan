# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600492
**Name:** Phan Xuân Quang Linh
**Date:** 15/04/2024

---

## 1. Ket qua thi nghiem

Chạy `agent_simulation.py` với hai bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Clean dataset có 3 record hợp lệ, không có lỗi kiểu, nên agent chọn đúng sản phẩm điện tử tốt nhất. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 3 | Dữ liệu có giá trị sai, category không nhất quán và bản ghi thiếu thông tin; agent vẫn trả lời nhưng kết quả không thực tế. |

---

## 2. Phan tich & nhan xet

Trong thí nghiệm này, dữ liệu sạch cho phép agent hoạt động đúng với logic đơn giản của nó: chọn sản phẩm điện tử có giá cao nhất. `processed_data.csv` đã loại bỏ các record không hợp lệ, giữ lại chỉ những mẫu có `price > 0` và `category` không rỗng, nên đầu vào cho mô phỏng là nhất quán và agent trả lời chính xác.

Ngược lại, `garbage_data.csv` chứa nhiều vấn đề về chất lượng dữ liệu.

- Duplicate IDs: `id` trùng nhau hoặc thiếu `id` khiến việc theo dõi và ghi nhớ record kém tin cậy.
- Sai kiểu dữ liệu: giá `ten dollars` không thể so sánh số học, làm cột `price` bị NaN trong pandas, nhưng vẫn có record `999999` đủ lớn để agent chọn.
- Giá trị cực đoan và outlier: `999999` là một giá trị vô lý trong ngữ cảnh sản phẩm tiêu dùng, khiến agent ưu tiên sai sản phẩm.
- Thiếu thông tin và null: một record có category trống, không thể dùng trong phân loại và lọc.

Tất cả những lỗi này làm giảm chất lượng “kiến thức” của agent. Mặc dù agent vẫn trả lời, câu trả lời trở nên không thực tế và thiếu ý nghĩa. Dữ liệu ô nhiễm đã làm méo thuật toán chọn lựa: thay vì chọn sản phẩm điện tử có giá hợp lý như Laptop hoặc Monitor, nó chọn Nuclear Reactor do giá lớn nhất, nhưng đây rõ ràng là lựa chọn sai trong bối cảnh câu hỏi.

Nhận xét chung: agent đơn giản phụ thuộc hoàn toàn vào chất lượng dữ liệu đầu vào. Nếu dữ liệu bị nhiễu, lỗi kiểu hoặc outlier, kết quả trả về sẽ trở nên kém chính xác dù prompt vẫn giống nhau.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Tôi đồng ý. Trong bài toán này, dữ liệu sạch và nhất quán quan trọng hơn prompt. Prompt vẫn giống nhau nhưng kết quả khác biệt rõ ràng do dữ liệu đầu vào. Vì vậy, chất lượng dữ liệu là yếu tố quyết định để agent trả lời chính xác và ổn định.

Kết luận: Trước khi tối ưu prompt hoặc logic mô hình, nên đảm bảo pipeline ETL loại bỏ dữ liệu xấu và chuẩn hóa dữ liệu đầu vào. Dữ liệu kém chất lượng sẽ làm giảm đáng kể hiệu quả của hệ thống AI dù prompt có tốt đến đâu.
