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
