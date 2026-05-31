---
title: "Báo cáo EDA"
date: "2026"
---


# 📊 1.1.3. Bài tập thực hành 1 – Rượu vang đỏ (Wine Quality)

## 🧪 Thực hiện thống kê mô tả

```python
def analyze(df):
    for col in df.columns:
        if np.issubdtype(df[col].dtype, np.number):

            print(f"""
Column: {col}

Mean: {np.mean(df[col])}
Median: {np.median(df[col])}
Mode: {stats.mode(df[col], keepdims=True).mode[0]}
Variance: {np.var(df[col])}
Std Dev: {np.std(df[col])}
Max: {np.max(df[col])}
Min: {np.min(df[col])}
60th Percentile: {np.percentile(df[col], 60)}
75th Percentile: {np.percentile(df[col], 75)}
Range: {np.max(df[col]) - np.min(df[col])}
IQR: {stats.iqr(df[col])}
Skewness: {stats.skew(df[col])}
Kurtosis: {stats.kurtosis(df[col])}
""")

    print("\n===== df.describe().T (CHECK) =====")
    display(df.describe().T.style.background_gradient(cmap="magma_r"))

print("\n===== wine =====")
analyze(wine)
```

## 🧾 Ghi ý nghĩa của đoạn code:

* Hàm `analyze(df)` dùng để thực hiện thống kê mô tả cho toàn bộ cột số trong dataset.
* Vòng lặp `for col in df.columns` giúp duyệt từng biến trong dữ liệu.
* Điều kiện `np.issubdtype(...)` đảm bảo chỉ xử lý dữ liệu dạng số (numeric), tránh lỗi với dữ liệu chữ.
* Các chỉ số thống kê được tính gồm:
  * **Mean, Median, Mode** → đo xu hướng trung tâm của dữ liệu
  * **Variance, Std Dev** → đo mức độ phân tán
  * **Min, Max, Range** → xác định biên dữ liệu
  * **Percentiles (60%, 75%)** → mô tả phân vị phân phối
  * **IQR** → phát hiện outlier
  * **Skewness** → độ lệch phân phối
  * **Kurtosis** → độ nhọn và mức độ outlier
* `df.describe().T` được dùng để so sánh nhanh kết quả thống kê chuẩn của pandas.
* `style.background_gradient()` giúp trực quan hóa bảng thống kê bằng màu sắc.

👉 Mục đích: hiểu đặc điểm phân phối từng biến và phát hiện bất thường trong dữ liệu rượu vang.
---------------------------------------------------------------------------------------------------------------------

# 📊 1.1.4. Bài tập thực hành 2 – Bệnh tiểu đường

## 🧪 Thực hiện thống kê mô tả

```python
print("\n===== diabetes =====")
analyze(diabetes)
```

## 🧾 Ghi ý nghĩa của đoạn code:

* Gọi lại hàm `analyze()` đã xây dựng ở bài trước.
* Áp dụng cho dataset **diabetes** (bệnh tiểu đường).
* Mục tiêu:
  * So sánh phân phối dữ liệu y tế với dữ liệu rượu vang
  * Hiểu đặc điểm các biến như glucose, BMI, age,...
* Giúp chuẩn bị dữ liệu cho bài toán phân loại (`Outcome`).

---

# 📊 1.2.3.1. EDA – Bệnh tiểu đường

## 🧪 Kiểm tra dữ liệu và trực quan hóa

```python
print("Missing values:\n", diabetes.isnull().sum())
print("Duplicate rows:", diabetes.duplicated().sum())

plt.figure(figsize=(6,5))
sns.countplot(x='Outcome', data=diabetes)
plt.title("Distribution of Diabetes Outcome")
plt.show()

diabetes.hist(figsize=(12,8), bins=20)
plt.suptitle("Feature Distributions")
plt.show()

key_features = ['Glucose', 'BMI', 'Age', 'BloodPressure']
for col in key_features:
    plt.figure(figsize=(8,5))
    sns.boxplot(x='Outcome', y=col, data=diabetes)
    plt.title(f'Outcome vs {col}')
    plt.show()

plt.figure(figsize=(10,6))
sns.heatmap(diabetes.corr(), annot=True, cmap='coolwarm')
plt.title("Correlation Matrix")
plt.show()
```

## 🧾 Ghi ý nghĩa của đoạn code:

* `isnull().sum()` → kiểm tra dữ liệu bị thiếu trong từng cột.
* `duplicated().sum()` → kiểm tra số dòng bị trùng lặp.
* `countplot(Outcome)` → kiểm tra sự cân bằng giữa:
  * 0: không mắc bệnh
  * 1: mắc bệnh
* `hist()` → hiển thị phân phối của tất cả biến số.
* `boxplot()`:
  * so sánh từng biến theo nhóm Outcome
  * giúp phát hiện biến quan trọng ảnh hưởng đến bệnh
* `heatmap(corr())`:
  * thể hiện mức độ tương quan giữa các biến
  * hỗ trợ chọn feature cho mô hình

👉 Mục tiêu: hiểu dữ liệu, tìm feature quan trọng và chuẩn bị cho machine learning.

---

# 📊 1.2.3.2. EDA – Dữ liệu Online Retail

## 🧪 Làm sạch và phân tích dữ liệu

```python
online_retail = online_retail[
    ['CustomerID','InvoiceNo','StockCode',
     'Quantity','UnitPrice','Description',
     'InvoiceDate','Country']
]

online_retail = online_retail[
    (online_retail['Quantity'] > 0) &
    (online_retail['UnitPrice'] > 0)
]

online_retail['TotalAmount'] = online_retail['Quantity'] * online_retail['UnitPrice']
online_retail['InvoiceDate'] = pd.to_datetime(online_retail['InvoiceDate'])

online_retail.isnull().sum()
online_retail.describe(include='all')
online_retail.info()
```

## 🧾 Ghi ý nghĩa của đoạn code:

* Lọc các cột cần thiết để phân tích bán hàng.
* Loại bỏ dữ liệu sai:
  * Quantity ≤ 0 (trả hàng)
  * UnitPrice ≤ 0 (lỗi dữ liệu)
* Tạo biến mới:
  * `TotalAmount` = doanh thu từng giao dịch
* Chuyển `InvoiceDate` sang datetime để phân tích theo thời gian.
* `isnull()` → kiểm tra missing data
* `describe()` → thống kê tổng quan
* `info()` → kiểm tra cấu trúc dữ liệu

👉 Mục tiêu: làm sạch dữ liệu và chuẩn bị cho phân tích kinh doanh.

---

## 📊 Phân tích theo quốc gia

```python
country_price = online_retail.groupby('Country')['Quantity'].sum().reset_index()
country_price = country_price.sort_values(by='Quantity', ascending=False)
```

## 🧾 Ý nghĩa:

* Gom nhóm theo quốc gia.
* Tính tổng số lượng sản phẩm bán ra.
* Sắp xếp để tìm quốc gia mua nhiều nhất.

---

## 📊 Top / Bottom countries

```python
top5 = country_price.head(5)
low5 = country_price.tail(5)
```

## 🧾 Ý nghĩa:

* Top 5 quốc gia tiêu thụ lớn nhất.
* Bottom 5 quốc gia tiêu thụ thấp nhất.

---

## 📊 Doanh thu theo năm

```python
online_retail['Year'] = online_retail['InvoiceDate'].dt.year
year_sales = online_retail.groupby('Year')['TotalAmount'].sum().reset_index()
```

## 🧾 Ý nghĩa:

* Trích xuất năm từ ngày hóa đơn.
* Tính tổng doanh thu theo từng năm.
* Dùng để phân tích xu hướng tăng trưởng.

---

## 📊 Khách hàng theo quốc gia

```python
cus_id = online_retail.groupby('Country')['CustomerID'].nunique().reset_index()
```

## 🧾 Ý nghĩa:

* Đếm số khách hàng duy nhất theo quốc gia.
* Tránh đếm trùng khách hàng.

---

## 📊 Phân tích sản phẩm

```python
avg_sales = online_retail.groupby(['StockCode','Description']).agg({
    'TotalAmount': 'sum',
    'Quantity': 'sum'
}).reset_index()
```

## 🧾 Ý nghĩa:

* Gom nhóm theo sản phẩm.
* Tính:
  * tổng doanh thu
  * tổng số lượng bán
* Xác định sản phẩm bán chạy.

---

## 📊 Dữ liệu cho visualization

```python
country_sales = online_retail.groupby('Country', as_index=False).agg({
    'Sales': 'sum',
    'Quantity': 'sum'
})
```

## 🧾 Ý nghĩa:

* Tổng hợp dữ liệu theo quốc gia.
* Chuẩn bị cho biểu đồ bản đồ (geo visualization).

---

# 📊 1.3.3. SweetViz – EDA tự động

```python
import sweetviz as sv

marketing_report = sv.analyze(marketing)
marketing_report.show_html()
```

## 🧾 Ý nghĩa:

* SweetViz tự động phân tích toàn bộ dataset.
* Tạo report HTML gồm:
  * phân phối dữ liệu
  * missing values
  * tương quan
* `show_html()` → xuất file báo cáo.

---

# 📊 1.3.4. AutoViz – EDA tự động

```python
from autoviz import AutoViz_Class

AV = AutoViz_Class()

dft = AV.AutoViz(
    "",
    dfte=marketing_data,
    verbose=0,
    chart_format="svg"
)
```

## 🧾 Ý nghĩa:

* AutoViz tự động sinh toàn bộ biểu đồ EDA.
* Không cần viết từng plot thủ công.
* Tự động:
  * histogram
  * scatter plot
  * correlation
* `verbose=0` → tắt log
* `chart_format="svg"` → biểu đồ nhẹ, rõ nét
