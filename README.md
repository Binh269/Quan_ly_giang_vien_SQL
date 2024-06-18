# Quản lý giảng viên 

Tác giả : Đỗ Thanh Bình
MSSV : K215480106137
Lớp : K57KMT

## Mô tả : 
  - Quản lý người dùng:
      + Người dùng bình thường : đăng nhập , xem lịch dạy học , đăng ký lịch dạy cho kỳ mới
      + Người quản lý : thêm, sửa , xóa thông tin giảng viên ;  liệt kê all , kiểm tra đăng ký lịch dạy của giảng viên
  - Quản lý lịch dạy : thêm , sửa, xóa lịch , phòng , giảng viên ( chỉ cho người quản lý ) ; liệt kê phòng dạy , ngày , giảng viên 
  - Quản lý buổi dạy của giảng viên : liệt kê môn dạy của giảng viên ; kiểm tra giảng viên có đi dạy hay không ( chỉ cho người quản lý )
  - Kiểm tra  : Tạo báo cáo giảng dạy của giảng viên , tìm kiếm giảng viên ( chỉ cho người quản lý ), kiểm tra lịch đăng ký dạy kì mới
  - Khi đăng ký kỳ dạy mới thì giảng viên đăng ký theo khoa của giảng viên và lịch dạy không được trùng ( khoa cảu giảng viên giống khoa của môn dạy ) và lịch dạy sẽ tự cập nhật , thay đổi theo môn đăng ký của giảng viên
### Thực hành
Thông tin cụ thể các bảng như sau  :
- Giảng viên: 🔑Id , mã giảng viên, tên giảng viên , họ tên , ngày sinh , giới tính , địa chỉ , số căn cước công dân , khoa .
- Môn: Id ,  🔑Mã môn, tên môn , số tín chỉ , khoa , ghi chú .
- Lớp: Id ,  🔑Mã lớp , tên lớp , số lương sinh viên , tiết , thứ , phòng .
- Khoa: Id , 🔑Mã khoa , tên khoa .
- Đăng nhập: 🔑Id  , user , password .
- Đăng ký dạy: 🔑Id , mã giảng viên , mã môn , mã lớp , học kỳ đăng ký .
- Lịch dạy: 🔑Id , mã giảng viên, mã môn , mã lớp , tiết , phòng .
  #### I. Tạo CSDL Quanly_giangvien trong hệ quản trị CSDL SQL Server
   ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/8aec4856-635d-45c5-9c47-a57ec5391dcc)
  
  -	Để tạo CSDL Quanly_giangvien : chuột phải vào “database” chọn “New database” => sau đó điền tên của CSDL vào Database name => click “OK” để xác nhận 
  #### II. Thiết kế bảng dữ liệu (Table)
  ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/79137894-853a-41a2-9fb2-cc038142c015)
  ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/24483a0a-492b-4ffc-a44b-3ede6224938a)
 ![Screenshot 2024-06-18 114637](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/9fad9ddc-c271-45fb-8b88-4d379c19ef9b)
![Screenshot 2024-06-18 114652](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/9456f3df-4d39-406c-93a7-969bbeb06ba9)


     1. Tạo bảng dữ liệu “Khoa” lưu trữ danh mục khoa
      Để tạo bảng chuột phải vào Table => New => Table => Ctrl + S để lưu và đặt tên
        ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/8dd5378d-641f-4ec5-bc1d-c8c279738f28)
        
      -	Cột “Makhoa” : Kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự trắng và các ký tự đặc biệt.
      -	Cột “id”  :đặt làm khóa chính (primary key) Kiểu dữ liệu ‘int’ + Không cho phép ‘null’ vì để id luôn là một giá trị duy nhất và không được phép trống 
      -	Cột “Tenkhoa”: để dữ liệu là ‘nvarchar(50)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ đến 50 ký tự.
    2. Thêm dữ liệu vào bảng Khoa
  
     	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/fd05e5a6-a30d-4afe-a7e4-05c9fc79549d)

      Để thêm dữ liệu chuột phải vào bảng cần thêm => chọn “Edit Top 200 Rows” sau đó thêm các dữ liệu vào .
      Hoặc sử dụng lệnh để thêm dữ liệu vào bảng như sau .
      ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/6a53900f-03ec-4411-8df3-d562b9da4d18)
  
    3. Tạo bảng dữ liệu “Mon” lưu trữ thông tin các môn học Monhoc có cấu trúc như sau:
      Để tạo bảng chuột phải vào Table => New => Table => Ctrl + S để lưu và đặt tên
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/201dd95f-8cf3-4545-9c7d-8d6a5a06f881)
       
      -	Cột “Mamon” : Kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự trắng và các ký tự đặc biệt.
      -	Cột “id”  :đặt làm khóa chính (primary key) Kiểu dữ liệu ‘int’ + Không cho phép ‘null’ vì để id luôn là một giá trị duy nhất và không được phép trống  
      -	Cột  “Tenmon” : để dữ liệu là ‘nvarchar(50)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ đến 50 ký tự.
      -	Cột  “Makhoa”: để kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự trắng và các ký tự           đặc biệt.
      -	Cột “Ghichu” : để dữ liệu là ‘nvarchar(Max)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ không giới hạn độ dài, đáp ứng nhu cầu lưu trữ thông tin chi tiết.
     4. Thêm dữ liệu vào bảng Mon
  
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/baa676a3-ae53-4254-9edb-a4a76337c111)

      Để thêm dữ liệu chuột phải vào bảng cần thêm => chọn “Edit Top 200 Rows” sau đó thêm các dữ liệu vào .Hoặc dùng lệnh sau để thêm :
      ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/7ac30f25-c52c-4e2e-acc8-d7a73e4acad4)
    5. Tạo bảng dữ liệu “Lop” lưu trữ danh mục lớp 
      Để tạo bảng chuột phải vào Table => New => Table => Ctrl + S để lưu và đặt tên
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/02e7c371-481d-4faf-acb0-6ef92cd410a3)
       
      Bảng này không đặt “Malop” làm khóa chính vì em muốn thêm dữ liệu để mỗi mã lớp có thể có nhiều tiết khác nhau và nhiều thứ khác nhau
      -	Cột “id”  : đặt làm khóa chính (primary key) để id không phụ thuộc vào bất kỳ thông tin nào (ví dụ như thông tin giáo viên), điều này làm giảm rủi ro khi cần thay đổi thông tin , việc bảo trì và tính toàn vẹn dữ liệu.
        o	  Kiểu dữ liệu ‘int’+ Không cho phép ‘null’ vì để id luôn là một giá trị duy nhất và không được phép trống 
      -	Cột  “Malop”: để kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự trắng và các ký tự         đặc biệt.
      -	Cột  “Tenlop” + “Phong”: để dữ liệu là ‘nvarchar(50)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ đến 50 ký tự.
      -	Cột “Soluongsv” + “Tiet” + “Thu”: để dữ liệu là int cho phép lưu trữ số nguyên.
    6. Thêm dữ liệu vào bảng Lop
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/f0169305-c31d-4ff2-8aa1-094623f9d1c7)

        Để thêm dữ liệu chuột phải vào bảng cần thêm => chọn “Edit Top 200 Rows” sau đó thêm các dữ liệu vào . Hoặc dùng lệnh sau để thêm :
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/3b2e9f61-8c8e-4957-83b1-004888b0546c)

    7.Tạo bảng dữ liệu “Giangvien”  lưu trữ thông tin giảng viên có cấu trúc như sau:
      Để tạo bảng chuột phải vào Table => New => Table => Ctrl + S để lưu và đặt tên
			![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/2a59cb60-a37d-4940-814e-1ada72d6d6de)
  
      -	Cột “Magv” : Kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự trắng và các ký tự đặc biệt.
      -	Cột “id”  :đặt làm khóa chính (primary key) Kiểu dữ liệu ‘int’ + Không cho phép ‘null’ vì để id luôn là một giá trị duy nhất và không được phép trống 
      -	Cột "Makhoagv": để kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự trắng                     và các ký tự đặc biệt.
      -	Cột “Hoten” + “Gioitinh” + “Dantoc” : để dữ liệu là ‘nvarchar(50)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ đến 50 ký tự.
      -	Cột “Ngaysinh” : để dữ liệu là ‘date’ cho phép thao tác và truy vấn dữ liệu liên quan đến ngày tháng năm một cách dễ dàng và chính xác.
      -	Cột “Diachi” : để dữ liệu là ‘nvarchar(Max)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ không giới hạn độ dài, đáp ứng nhu cầu lưu trữ thông tin chi tiết.
      -	Cột “So_cccd” : để kiểu dữ liệu là ‘VARCHAR(12)’ để lưu trữ 12 ký tự do số cccd là 12 số và để tránh mất mát thông tin khi có các giá trị 0 đứng đầu và vẫn lưu trữ cccd cũ là 9 số mà không bị xung đột.
    8. Thêm dữ liệu vào bảng Giangvien
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/8c7cd01e-9a0f-4b73-ac53-9f08a94b6f1d)

      Để thêm dữ liệu chuột phải vào bảng cần thêm => chọn “Edit Top 200 Rows” sau đó thêm các dữ liệu vào . Hoặc dùng lệnh sau để thêm :
      ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/26880776-8a33-47d5-8bab-7b1eca280181)
    9. Tạo bảng dữ liệu “Dangnhap” lưu trữ danh mục đăng nhập 
      Để tạo bảng chuột phải vào Table => New => Table => Ctrl + S để lưu và đặt tên
      ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/0725a824-bde1-4ba0-bdc0-4bf0e20d8c40)

      -	Cột “id”  : đặt làm khóa chính (primary key) để id không phụ thuộc vào bất kỳ thông tin nào (ví dụ như thông tin giáo viên), điều này làm giảm rủi ro khi cần thay đổi thông tin , việc bảo trì và tính toàn vẹn dữ liệu.
      -	Cột  “user” + “password” để kiểu dữ liệu là ‘VARCHAR(64)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 64 ký tự, bao gồm cả ký tự trắng và         các ký tự đặc biệt.
    10. Thêm dữ liệu vào bảng Dangnhap
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/b4eedc94-2abe-4416-8df1-fa3e4f977bdb)

      Để thêm dữ liệu chuột phải vào bảng cần thêm => chọn “Edit Top 200 Rows” sau đó thêm các dữ liệu vào .
    11. Tạo bảng dữ liệu “Dangkyday” lưu trữ danh mục đăng ký dạy 
      Để tạo bảng chuột phải vào Table => New => Table => Ctrl + S để lưu và đặt tên
      ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/ddbc7e8f-40f4-4f2a-9bcc-02bb4d21bbd8)

      -	Cột “id”  : đặt làm khóa chính (primary key) để id không phụ thuộc vào bất kỳ thông tin nào (ví dụ như thông tin giáo viên), điều này làm giảm rủi ro khi cần thay đổi thông tin , việc bảo trì và tính toàn vẹn dữ liệu.
        o Kiểu dữ liệu ‘int’ + Không cho phép ‘null’ vì để id luôn là một giá trị duy nhất và không được phép trống 
      -	Cột  “Magv” + “Mamon” + “Malop”: để kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự         trắng và các ký tự đặc biệt.
      -	Cột “Hockydk” : để dữ liệu là ‘nvarchar(50)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ đến 50 ký tự.
    12. Thêm dữ liệu vào bảng Dangkyday
       ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/5f68f584-d9c0-4fd0-ad69-45f08ef4f33c)

      - Để thêm dữ liệu chuột phải vào bảng cần thêm => chọn “Edit Top 200 Rows” sau đó thêm các dữ liệu vào .
      - Do em muốn là giảng viên khoa nào thì chỉ được dạy môn của khoa đó và lớp khoa nào thì mới đăng ký được môn của khoa đó ( do không kết hợp với đăng ký môn học của sinh viên nên lớp của từng môn cụ thể của các khoa em điền ngẫu nhiên ạ) và khi giảng viên đăng kí         môn dạy và lớp dạy thì lịch học không được trùng nhau . Do đó em sẽ tạo ra 1 trigger tên là kiemtra_dangkyday
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/968ee3e9-0766-4fc0-a276-ea75126a6ca6)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/e0aedf61-198f-45b6-b062-d8c10b351808)

      Test kiểm tra nếu giảng viên đăng ký khác khoa
      ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/b0e47638-6c14-45d3-a423-be8909ff17ce)
  
	Sau khi đã có trgger để lọc dữ liệu đầu vào cho chuẩn xác thì em sẽ tự thêm dữ liệu để phù hợp .
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/e6501e97-09f6-4fc5-b67b-2a22f891a954)

    13. Tạo bảng dữ liệu “Lichday” lưu trữ danh mục lịch dạy học 
      Để tạo bảng chuột phải vào Table => New => Table => Ctrl + S để lưu và đặt tên
      ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/2ecf91a4-2d7e-4640-a0ae-bb8faa6355b3)

      -	Cột “id”  : đặt làm khóa chính (primary key) để id không phụ thuộc vào bất kỳ thông tin nào (ví dụ như thông tin giáo viên), điều này làm giảm rủi ro khi cần thay đổi thông tin , việc bảo trì và tính toàn vẹn dữ liệu.
        o	  Kiểu dữ liệu ‘int’ + Không cho phép ‘null’ vì để id luôn là một giá trị duy nhất và không được phép trống 
      -	Cột  “Magv” + “Mamon” để kiểu dữ liệu là ‘VARCHAR(20)’ để tối ưu bộ nhớ vì khi dùng bao nhiêu ký tự thực tế thì bộ nhớ chỉ cấp phát từng ấy và thêm 1 byte để lưu trữ độ dài chuỗi . Cho phép lưu trữ các mã có độ dài lên đến 20 ký tự, bao gồm cả ký tự trắng và           các ký tự đặc biệt.
      -	Cột “Phong” : để dữ liệu là ‘nvarchar(50)’ cho phép lưu trữ ký tự Unicode, thích hợp cho tên có các ký tự đặc biệt để dùng tiếng việt có dấu và cho phép lưu trữ đến 50 ký tự.
      -	Cột “Tiet”: để dữ liệu là int cho phép lưu trữ số nguyên.
      -	Cột “Ngay” : để dữ liệu là ‘date’ cho phép thao tác và truy vấn dữ liệu liên quan đến ngày tháng năm một cách dễ dàng và chính xác.
    14. Thêm dữ liệu vào bảng Lichday
        Để phù hợp với mô tả ở trên em đã viết thêm 1 trigger update_lichday để khi có sự chèn hay cập nhật trong bảng dangkyday khi giảng viên đăng ký môn thì bảng lịch học sẽ tự động cập nhật. 
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/7b82628b-2406-4a74-b217-428d95a290ec)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/c91c594c-31ce-4b26-88dd-9b175039b832)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/8768abf0-0e1c-4464-a934-22c60572d6c2)

    15. Tạo thủ tục tìm kiếm thông tin giảng viên bằng một trong các thông tin : mã giảng viên , tên giảng viên , mã khoa , tên khoa
        ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/4e3dc408-1356-4681-807a-c7d29bb7f730)

    16. Tạo FUntion tìm kiếm những giảng viên chưa đăng ký dạy kỳ mới
        ![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/84b5aa98-1e11-4c1f-8e47-10dd7a1d5c41)

    17. Tạo cursor để phân quyền tài khoản
        id là 1 thì cho xem , sửa tất cả tài khoản mạt khẩu.
        id là 2, 3 thì cho xem , sửa những tài khoản mật khẩu từ 3 trở đi.
        các id khác không xem ,sửa được .
        - Trước hết cần tạo một bảng 
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/54c56566-3681-47c2-885f-10cb7f6f1514)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/0e7d5bbe-891e-4ad1-9bfc-baa6f7b6bd6e)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/cef281fe-b148-403b-8963-381ec19bc9be)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/f1ed3b76-472a-4ab0-afe2-593e8d1ac8aa)

	Test kết quả :
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/99f751c6-ecf0-4010-8fa7-5f8f0cad509a)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/a87b9b8a-34aa-406a-95b3-b8769418981b)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/88697136-2e24-4194-ae7b-46dbe709d866)
	![image](https://github.com/Binh269/Quan_ly_giang_vien_SQL/assets/147959501/185df343-4afd-438b-90ce-62fccd22bee6)







