# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600830
**Name:** Vũ Tuấn Hoàng
**Date:** 10/6/2026 

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 10 | Gợi ý chính xác dựa trên sản phẩm hợp lệ, có giá hợp lý nhất. |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Gợi ý sản phẩm không hợp lý do dữ liệu chứa outlier sai lệch nghiêm trọng. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai do logic của nó phụ thuộc hoàn toàn vào dữ liệu đầu vào. Khi sử dụng Garbage Data, dữ liệu không được làm sạch nên chứa các giá trị dị biệt (outliers) hoặc thông tin rác. Ví dụ trong trường hợp này, "Nuclear Reactor" (lò phản ứng hạt nhân) được liệt kê với giá trị lên tới 999999, một con số phi lý đối với hàng điện tử tiêu dùng nhưng lại vượt mặt các sản phẩm thật do agent được cấu hình để tìm kiếm sản phẩm đắt nhất. Dữ liệu sai lệch (không kiểm tra khoảng giá hợp lệ hay loại sản phẩm thực tế) đã dẫn đến việc AI đưa ra lời khuyên vô lý. Ngoài ra, việc thiếu kiểm soát null values, bản ghi trùng lặp (Duplicate IDs), hay sai kiểu dữ liệu có thể làm hỏng các bộ lọc tìm kiếm của AI, dẫn tới kết quả chệch hướng hoàn toàn khỏi thực tế. Dữ liệu rác sẽ làm sai lệch mọi mô hình máy học.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý.

Một prompt dù có chi tiết và hoàn hảo đến đâu cũng không thể khắc phục được hậu quả của dữ liệu sai lệch, vì AI sử dụng dữ liệu làm "tri thức" nền tảng để trả lời. Nếu dữ liệu đầu vào là rác ("Garbage In"), thì kết luận đầu ra cũng sẽ là rác ("Garbage Out"), bất kể cách đặt câu hỏi tinh vi ra sao. Do đó, làm sạch và đảm bảo dữ liệu chất lượng là yếu tố cốt lõi quyết định độ tin cậy của Agent.
