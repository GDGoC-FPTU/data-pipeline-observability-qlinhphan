[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574107&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** qlinhphan@gmail.com
**Name:** Phan Xuân Quang Linh

**Student Email:** ai20k-2a202600492@student.fpt.edu.vn
**Name:** Phan Xuân Quang Linh

---

## Mo ta

(Mo ta ngan gon bai lab va nhung gi ban da lam)
Bài lab này hướng dẫn xây dựng một pipeline ETL tự động để xử lý dữ liệu sản phẩm từ file JSON. Pipeline thực hiện các bước: đọc dữ liệu, kiểm tra và loại bỏ các record không hợp lệ (giá <= 0 hoặc thiếu category), chuẩn hóa category, tính giá sau giảm giá 10%, thêm metadata thời gian xử lý và xuất ra file CSV. Sau đó, sử dụng agent mô phỏng để kiểm tra tác động của chất lượng dữ liệu đến kết quả trả lời của AI agent.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Mo ta cach ban chay thi nghiem Clean vs Garbage data
python agent_simulation.py
# Script sẽ tự động test với cả dữ liệu sạch (processed_data.csv) và dữ liệu lỗi (garbage_data.csv).
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── solution.py              # ETL Pipeline script
├── agent_simulation.py      # Script mô phỏng agent trả lời
├── processed_data.csv       # Output đã xử lý
├── garbage_data.csv         # Dữ liệu lỗi để stress test
├── experiment_report.md     # Báo cáo thí nghiệm
├── raw_data.json            # Dữ liệu gốc
├── README.md                # File này
└── tests/                   # Thư mục test autograder
```

---

## Ket qua

(Tom tat ket qua: bao nhieu records da xu ly, bao nhieu bi loai, v.v.)
Số record đầu vào: 5 (raw_data.json)
Số record hợp lệ sau ETL: 3
Số record bị loại: 2 (do price <= 0 hoặc thiếu category)
File processed_data.csv gồm các cột: id, product, price, category, discounted_price, processed_at

Ví dụ output agent:

```
Testing with CLEAN data:
Agent: Based on my data, the best choice is Laptop at $1200.

Testing with GARBAGE data:
Agent: Based on my data, the best choice is Nuclear Reactor at $999999.
```

Pipeline đã loại bỏ hiệu quả dữ liệu xấu, giúp agent trả lời chính xác hơn với dữ liệu sạch. Khi dùng dữ liệu lỗi, agent trả về kết quả không thực tế, cho thấy tầm quan trọng của chất lượng dữ liệu đầu vào đối với hệ thống AI.
