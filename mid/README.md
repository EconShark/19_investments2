# Xây dựng dashboard thông tin đầu tư có hỗ trợ Chatbot – Assignment

## Thông tin chung
- **Ngày mở:** Monday, 1 June 2026, 12:00 AM  
- **Hạn nộp:** Sunday, 16 August 2026, 11:59 PM  

## Yêu cầu chung
Sinh viên dựa trên code mẫu để xây dựng một Financial Dashboard bao gồm:
- Một tài sản tài chính (cổ phiếu, trái phiếu, bitcoin, v.v.)
- Danh mục đầu tư
- Chatbot hỗ trợ phân tích tài chính

---

## 1. Dashboard cho một tài sản

### [1] Summary
Hiển thị thông tin tổng quan của tài sản được chọn trong danh sách:
- Cổ phiếu (Việt Nam hoặc quốc tế)
- Trái phiếu
- Bitcoin hoặc các crypto

Nội dung:
- Giá hiện tại
- Mức thay đổi (%)
- Khối lượng giao dịch
- Các chỉ số cơ bản (nếu có)

---

### [2] Chart
Hiển thị biến động giá và khối lượng giao dịch theo thời gian.

Yêu cầu:
- Chọn khoảng thời gian: ngày, tuần, tháng, tùy chỉnh
- Loại biểu đồ:
  - Line chart
  - Candlestick chart
  - Volume chart

---

### [3] Thống kê và phân tích tài chính
Phân tích định lượng cho tài sản:

- Return:
  - Daily return
  - Log return
- Risk:
  - Volatility
  - Standard deviation
- Phân phối lợi suất:
  - Histogram
- Chỉ báo kỹ thuật (nếu có):
  - Moving average
  - RSI
  - MACD

---

## 2. Phân tích danh mục đầu tư

### [4] Portfolio Analysis
- CAPM:
  - Beta
  - Expected return
  - Phân tách risk (systematic / idiosyncratic)
- APT (Arbitrage Pricing Theory)
- Các chỉ số hiệu suất:
  - Sharpe ratio
  - Sortino ratio
  - Maximum drawdown

Biểu đồ:
- Efficient frontier
- Heatmap tương quan
- Phân bổ danh mục (pie chart)

---

### [5] Monte Carlo Simulation
Mô phỏng giá trị danh mục tương lai:

- Phân phối giá trị danh mục
- Value at Risk (VaR)
- Expected shortfall
- Các kịch bản:
  - Best case
  - Worst case
  - Random paths

---

## 3. Chatbot hỗ trợ

### Chức năng
Chatbot hỗ trợ trả lời:
- Giá tài sản
- Hiệu suất danh mục
- Rủi ro đầu tư
- Giải thích chỉ số tài chính

### Ví dụ câu hỏi
- Cổ phiếu này rủi ro như thế nào?
- Danh mục có tối ưu không?
- Sharpe ratio là gì?

---

## Deliverables
Sinh viên nộp:
- Slide thuyết trình
- Báo cáo
- Code dự án