# _BÁO CÁO ĐỒ ÁN CUỐI KÌ

## Cấu trúc folder đồ án
- `notebook/`: chứa Jupyter Notebook
- `images/`: chứa hình ảnh biểu đồ
- `data/`: chứa file Excel
- `README.md`: báo cáo chính của nhóm

## 1. Thành viên nhóm
- Vũ Lê Hoàng Nhất. MSSV: 051206008093
- Thiệu Hồng Trang. MSSV: 080306001468
- Thái Minh Quân. MSSV: 034206006683
- Võ Đức Thịnh. MSSV: 060206008313
- Trương Thanh Thảo. MSSV: 052306007155

## 2. Phân công công việc
- Nhất, Trang: Xử lí và Khám phá dữ liệu
- Quân : Phân tích thống kê tổng quan
- Thịnh: Vẽ biểu đồ
- Thảo: Tạo file excel thô, phân tích và máy học
## 3. Các bước thực hiện
- Tạo file excel thô
- Khám phá các dữ liệu có trong file
- Xử lí dữ liệu
- Phân tích dữ liệu
- vẽ biểu đồ
- Áp dụng thuật toán máy học
## 4. Chi tiết
### 4.1 Tạo file excel thô bằng python
```python
import pandas as pd
import numpy as np
import random

#tạo số dòng dữ liệu
so_du_lieu= 2400

#tạo dữ liệu mẫu
names=['Lê Thị A','Võ Văn B','Lê Văn C','Phạm Minh D', 'Nguyễn Thị E',0, None]
ages=[18,19,21,22,'hai mươi',None]
genders=['nam','nữ','Nam','Nữ','Khác',None]
majors=['HTTTQL','CNTT','Kế toán','Logistic',None]
cities=['Hà Nội','Tp.HCM','Đà Nẵng','Phan Thiết',00,'Cà Mau', None]
emails=['abc1@gmail.com','abc2@gmail','123email.com','xyz123@@','user123@.com',None]
phones=['0123456789','123b567c89','098abc4321','081 234 6579',None]
grades=[8.5,9.5,9,8,'bảy',100,None]
scholarship=[True,False,'Có','Không',None]
notes=['Học tốt','Chưa đóng học phí','Thiếu giấy tờ',1,'Sai thông tin','Đã đóng học phí','Chưa đạt',None]

#hàm ngày/tháng/năm
def random_date():
    dates=['%d-%m-%Y','%d/%m/%Y',None]
    ax=random.choice(dates)
    #kiểm tra xem biến có None thật không
    if ax is None:
        return None
    return (pd.to_datetime('2024-01-01')+pd.to_timedelta(random.randint(0,180), unit='D')).strftime(ax)

#tạo dữ liệu DataFrame
data={
    'Tên':[random.choice(names) for _ in range(du_lieu)],
    'Tuổi':[random.choice(ages) for _ in range(du_lieu)],
    'Giới tính':[random.choice(genders) for _ in range(du_lieu)],
    'Ngày đăng ký':[random_date() for _ in range (du_lieu)],
    'Chuyên ngành':[random.choice(majors) for _ in range(du_lieu)],
    'Thành phố':[random.choice(cities) for _ in range (du_lieu)],
    'Email':[random.choice(emails) for _ in range(du_lieu)],
    'SĐT':[random.choice(phones) for _ in range (du_lieu)],
    'Điểm TB':[random.choice(grades) for _ in range(du_lieu)],
    'Học bổng':[random.choice(scholarship) for _ in range(du_lieu)],
    'Ghi chú':[random.choice(notes) for _ in range(du_lieu)],
    'Cột dư': ['Không']*du_lieu
}
        
#tạo bảng dữ liệu
sv = pd.DataFrame(data)
sv.to_excel("Danh_sach_sinh_vien.xlsx", index=False)
print(' Đã tạo file Excel thành công!')
```
### 4.2 Khám phá dữ liệu
-Với 2400 dòng dữ liệu và 12 cột

![2400 dòng và 12 cột](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_28.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_29.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_30.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_31.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_32.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_33.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_34.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_35.png?raw=true)

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_36.png?raw=true)

### 4.3 Xử lí dữ liệu
-Đầu tiên ta chuẩn hóa kiểu dữ liệu cho 'Thành phố' và 'Tên' thành kiểu dữ liệu chuỗi.
```python
df['Thành phố'] = df['Thành phố'].astype(str).replace(["0", "nan"], np.nan)
df['Tên'] = df['Tên'].astype(str).replace(["0", "nan"], np.nan)
```
-Chuẩn hóa các cột tiếp theo ('SĐT', 'Tuổi', 'Email')
```python
df['Thành phố'] = df['Thành phố'].astype(str).replace(["0", "nan"], np.nan)
df['Tên'] = df['Tên'].astype(str).replace(["0", "nan"], np.nan)
```
-Chuẩn hóa các cột khác
```python
df['Email'] = df['Email'].apply(lambda x: x if str(x).endswith("@gmail.com") else np.nan)
df['SĐT'] = df['SĐT'].apply(lambda x: x if len(str(x)) == 10 and str(x).isdigit() else np.nan)
df['Ghi chú'] = df['Ghi chú'].replace(1, np.nan)

def clean_age(age):
    try:
        return int(age)
    except:
        return np.nan
df['Tuổi'] = df['Tuổi'].apply(clean_age)

df['Giới tính'] = df['Giới tính'].apply(
    lambda x: "Nữ" if str(x).strip().lower() == "nữ" else
              ("Nam" if str(x).strip().lower() == "nam" else np.nan)
)

df['Ngày đăng ký'] = pd.to_datetime(df['Ngày đăng ký'], errors='coerce').dt.strftime('%d/%m/%Y')
```
-Xử lí giá trị cột 'điểm TB' cho phù hợp
```python
def clean_score(score):
    try:
        score = float(score)
        # Kiểm tra giá trị nằm trong khoảng từ 0 đến 10
        if 0 <= score <= 10:
            return score
        else:
            return np.nan
    except:
        return np.nan

df['Điểm TB'] = df['Điểm TB'].apply(clean_score)

df['Học bổng'] = df['Học bổng'].replace({False: "Không", True: "Có"})
```
-Xóa "cột dư" khỏi DataFrame
```python
columns_to_drop = ['Cột dư']  # Tên cột bạn muốn xóa
df = df.drop(columns=columns_to_drop, errors='ignore')
```
-Chuyển giá trị trong cột 'Tuổi' thành số nguyên
```python
df['Tuổi'] = df['Tuổi'].fillna(df['Tuổi'].mean()).astype(int)  # Dùng .astype(int) để chuyển đổi thành số nguyên.
df["Giới tính"] = df["Giới tính"].apply(lambda x: random.choice(["Nam", "Nữ"]) if x == "Không rõ" else x)
```
-Điền các giá trị còn thiếu vào các ô trống
```python
# Điền giá trị mặc định "01/04/2024" cho các ô trống trong cột "Ngày đăng ký"
df['Ngày đăng ký'] = df['Ngày đăng ký'].fillna('01/04/2024')
import random

# Điền giá trị ngẫu nhiên "HTTTQL" hoặc "Ngôn Ngữ Anh" cho ô trống trong cột "Chuyên ngành"
df['Chuyên ngành'] = df['Chuyên ngành'].apply(lambda x: random.choice(["HTTTQL", "Ngôn Ngữ Anh"]) if pd.isnull(x) or x == '' else x)

# Điền giá trị ngẫu nhiên "Quảng Ngãi" hoặc "Bình Định" vào các ô trống trong cột "Thành phố"
df['Thành phố'] = df['Thành phố'].apply(lambda x: random.choice(["Quảng Ngãi", "Bình Định"]) if pd.isnull(x) or x == '' else x)

# Điền giá trị ngẫu nhiên vào các ô trống trong cột "Email"
df['Email'] = df['Email'].apply(lambda x: random.choice(['xyz234@gmail.com', 'def5@gmail.com']) if pd.isnull(x) or x == '' else x)

# Danh sách các tên
ten_ngau_nhien = ["Võ Thị A", "Nguyễn Thanh C", "Trần Văn D", "Phạm Thị B", "Lê Văn E"]

# Điền giá trị ngẫu nhiên vào các ô trống trong cột "Tên"
df['Tên'] = df['Tên'].apply(lambda x: random.choice(ten_ngau_nhien) if pd.isnull(x) or x == '' else x)

# Danh sách các tên mới
ten_moi = ["Nguyễn Văn G", "Trần Thị H", "Phạm Minh K", "Lê Thị M", "Võ Văn T"]

# Thay thế các giá trị "D", "A", và "E" bằng các tên mới trong danh sách
df['Tên'] = df['Tên'].apply(lambda x: random.choice(ten_moi) if x in ["D", "A", "E"] else x)

# Điền giá trị ngẫu nhiên vào các ô trống trong cột "Điểm TB"
df['Điểm TB'] = df['Điểm TB'].apply(lambda x: random.choice([8, 9, 9.5]) if pd.isnull(x) or x == '' else x)

# Điền giá trị "Không" vào các ô trống trong cột "Học bổng"
df['Học bổng'] = df['Học bổng'].fillna('Không')

# Điền giá trị ngẫu nhiên vào các ô trống trong cột "Ghi chú"
df['Ghi chú'] = df['Ghi chú'].apply(lambda x: random.choice(['Bài viết rất tốt', 'Hoàn thành xuất sắc']) if pd.isnull(x) or x == '' else x)

# Tạo danh sách các số điện thoại tương tự
so_dien_thoai_ngau_nhien = ["0147485950", "0912356789", "0987654321", "0901234567", "0123456789"]

# Sửa đổi các số trong cột "SĐT" hoặc điền ngẫu nhiên
df['SĐT'] = df['SĐT'].apply(lambda x: random.choice(so_dien_thoai_ngau_nhien) if pd.isnull(x) or x == '' else random.choice(so_dien_thoai_ngau_nhien))
```
-Dựa vào tên để điền giới tính
```python
# Dựa vào tên để điền rõ giới tính
df['Giới tính'] = df['Tên'].apply(lambda x: 'Nữ' if 'Thị' in x else 'Nam')

# Kiểm tra kết quả
print(df[['Tên', 'Giới tính']])
```
-Đánh Labelling
```python
# Gán nhãn cho cột "Học bổng"
df['Label Học bổng'] = df['Học bổng'].apply(lambda x: "Được học bổng" if x == "Có" else "Không có học bổng")
# Thêm số "0" vào đầu các số trong cột "SĐT" nếu chưa có
df['SĐT'] = df['SĐT'].apply(lambda x: '0' + str(x) if not str(x).startswith('0') else str(x))

# Kiểm tra kết quả
print(df[['Học bổng', 'Label Học bổng']].head())
```
-Lưu file
```python
# Lưu dữ liệu vào file Excel
df.to_excel("File_Hoan_Chinh.xlsx", index=False)
```
### 4.4 Phân tích tổng quan
-Phân tích theo thống kê tổng quan
```python
# a) Số lượng sinh viên
so_luong_sinh_vien = len(df)
print("a) Số lượng sinh viên:", so_luong_sinh_vien)

# b) Số lượng sinh viên mỗi chuyên ngành
sv_moi_chuyen_nganh = df['Chuyên ngành'].value_counts()
print("\nb) Số lượng sinh viên mỗi chuyên ngành:")
print(sv_moi_chuyen_nganh)

# c) Tỉ lệ sinh viên có học bổng
ti_le_hoc_bong = (df['Học bổng'] == 'Có').mean() * 100
print(f"\nc) Tỉ lệ sinh viên có học bổng: {ti_le_hoc_bong:.2f}%")

# d) Số sinh viên chưa đóng học phí
so_sv_chua_dong_hoc_phi = df['Ghi chú'].str.contains('Chưa đóng học phí', na=False).sum()
print("d) Số sinh viên chưa đóng học phí:", so_sv_chua_dong_hoc_phi)
```
-Phân tích theo độ tuổi
```python
# a) Tuổi lớn nhất
tuoi_lon_nhat = df['Tuổi'].max()
print("\n3.2 a) Tuổi lớn nhất:", tuoi_lon_nhat)

# b) Tuổi nhỏ nhất
tuoi_nho_nhat = df['Tuổi'].min()
print("3.2 b) Tuổi nhỏ nhất:", tuoi_nho_nhat)
```
### 4.3 Xử lí imblance và Lưu dữ liệu vào database
### Sau khi khám phá, xử lí dữ liệu cho chuẩn và phân tích tổng quan, ta thấy số sinh viên "Có học bổng" ít hơn nhiều so với "Không học bổng" -> Mô hình bị lệch
--Dữ liệu trước khi cân bằng

![Trước khi imblance](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_12.png?raw=true)

### Sử dụng kĩ thuật Oversampling bằng SMOTE từ thư viện imblearn nhằm: tăng dữ liệu "Có học bổng", cân bằng
-Dữ liệu sau khi imblance bằng SMOTE và lưu vào database

![Sau khi imblance và lưu vào database](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_13.png?raw=true)

![Sau khi imblance và lưu vào database](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_14.png?raw=true)

### 4.4 Vẽ biểu đồ trực quan

![Biểu đồ (cột) sinh viên theo chuyên ngành](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_2.png?raw=true)

![Biểu đồ (tròn) tỉ lệ sinh viên có học bổng](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_3.png?raw=true)

-Vẽ các biểu đồ

![Biểu đồ (Histogram) phân bố điểm TB](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_4.png?raw=true)

![Biểu đồ (Barplot) so sánh học bổng theo thành phố](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_5.png?raw=true)

![Biểu đồ (Pie chart) tỉ lệ sinh viên theo giới tính](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_6.png?raw=true)

![Biểu đồ (cột) số sinh viên có học bổng theo chuyên ngành](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_7.png?raw=true)

![Biểu đồ (Ngang: Horizontal barplot) số lượng sinh viên theo thành phố](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_8.png?raw=true)

![Biểu đồ (Line) số lượng sinh viên theo thời gian](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_9.png?raw=true)

![Biểu đồ (Scatter) mối liên hệ giữa tuổi và điểm TB](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_10.png?raw=true)

![Biểu đồ (Heat map) tương quan giữa các cột số](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_11.png?raw=true)

### 4.5 Lọc các dữ liệu
-Lọc cột "Ghi chú" Có học bổng và "Điểm TB" trên 9.0

![Lọc có học bổng và điểm trên 9.0](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_22.png?raw=true)

-Lọc 4 điều kiện: có học bổng + điểm TB trên 9.0 + ghi chú học tốt hoặc Hoàn thành xuất sắc

![Lọc 4 điều kiện](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_23.png?raw=true)

### 4.5 Phân tích tương quan giữa học lực dựa trên Điểm TB và việc đóng học phí
### Tạo thêm các đặc trưng giúp phân nhóm dễ theo dõi hơn

![Phân tích tương quan](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_24.png?raw=true)

### Ta thấy được học lực cao thì tỉ lệ đóng học phí cũng cao

### 4.6 Chuyển Điểm TB sang GPA

![GPA](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_25.png?raw=true)


### 4.7 Thuật toán máy học
-Mô hình Random Forest
### Dùng thuật toán Random Forest để huấn luyện mô hình phân loại sinh viên đạt học bổng (label)
### Mô hình mạnh mẽ, dễ hiểu, không cần chuẩn hóa dữ liệu.
### Có thể cho biết yếu tố nào quan trọng nhất trong quyết định có học bổng.

![Random Forest](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_15.png?raw=true)

-Mô hình KNN

![KNN](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_17.png?raw=true)

-Mô hình SVM

![SVM](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_27.png?raw=true)

-So sánh 3 thuật toán: Random Forest, KNN, SVM

![SVM](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_18.png?raw=true)

![SVM](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_19.png?raw=true)

![SVM](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_20.png?raw=true)

-Phân cụm bằng KMeans

![Kmeans](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_16.png?raw=true)

-Thuật toán Liner Regression

![L G](https://github.com/Thanhthao-hub/B-o-c-o-cu-i-k-/blob/main/images/Screenshot_21.png?raw=true)


