# _BÁO CÁO ĐỒ ÁN CUỐI KÌ

## Cấu trúc folder đồ án
- `notebook/`: chứa Jupyter Notebook
- `images/`: chứa hình ảnh biểu đồ
- `report/`: chứa báo cáo Word/PDF
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
-Với 2400 dòng dữ liệu, thông tin đa dạng nhưng còn thô, chưa sạch, thiếu thông tin
### 4.3 Xử lí dữ liệu
-Đầu tiên ta chuẩn hóa kiểu dữ liệu cho Thành phố và Tên thành kiểu dữ liệu chuỗi.
```python
df['Thành phố'] = df['Thành phố'].astype(str).replace(["0", "nan"], np.nan)
df['Tên'] = df['Tên'].astype(str).replace(["0", "nan"], np.nan)
```
-Chuẩn hóa các cột tiếp theo (SĐT, Tuổi, Email)
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
-Xử lí giá trị cột điểm TB cho phù hợp
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
-Xóa cột dư khỏi DataFrame
```python
columns_to_drop = ['Cột dư']  # Tên cột bạn muốn xóa
df = df.drop(columns=columns_to_drop, errors='ignore')
```
-

-
