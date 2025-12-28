# Maven Toys – Sales Overview Dashboard

## 1. Tổng quan
Dự án này tập trung phân tích dữ liệu bán hàng và quản lý hàng tồn kho của chuỗi cửa hàng đồ chơi giả định **Maven Toys** tại Mexico.  
Dashboard được xây dựng bằng **Power BI** nhằm cung cấp cái nhìn tổng quan về hiệu quả kinh doanh, xu hướng doanh thu theo thời gian, hiệu suất theo cửa hàng và khả năng sinh lợi của sản phẩm.

---

## 2. Bộ dữ liệu
Bộ dữ liệu được cung cấp bởi **Maven Analytics**, mô phỏng dữ liệu bán hàng và quản lý hàng tồn kho của chuỗi cửa hàng đồ chơi giả định Maven Toys tại Mexico.

- Thời gian dữ liệu: từ **01/01/2022** đến **30/09/2023**
- Các bảng dữ liệu chính:
  - **Sales**: thông tin đơn hàng, số lượng bán
  - **Products**: thông tin sản phẩm, giá bán và giá vốn
  - **Stores**: thông tin cửa hàng và vị trí
  - **Inventory**: số lượng tồn kho theo cửa hàng
  - **Calendar**: bảng thời gian phục vụ phân tích theo ngày, tháng, năm

---

## 3. Modeling
Dữ liệu được thiết kế theo mô hình **Star Schema** nhằm tối ưu hiệu suất và khả năng phân tích trong Power BI.

<img width="1095" height="557" alt="image" src="https://github.com/user-attachments/assets/0f1d908b-0c24-4625-ad5d-765314daeb3f" />


---

## 4. Xử lý dữ liệu & DAX

Bảng **Sales** ban đầu không có sẵn các thông tin về **Cost**, **Revenue** và **Profit**.  
Do đó, các chỉ số này được tính toán bổ sung dựa trên số lượng bán và thông tin giá sản phẩm từ bảng **Products**.

Cost =
sales[Units] * RELATED ( products[Product_Cost] )

Revenue =
sales[Units] * RELATED ( products[Product_Price] )

Profit =
sales[Revenue] - sales[Cost]

---
## 5. Trực quan hóa với Power PI
### 5.1. OverView
<img width="1376" height="772" alt="image" src="https://github.com/user-attachments/assets/ff6b1dc8-465c-4675-a7bd-2d45931f7c16" />

---

- Tổng doanh thu tính đến nay là 14,44 triệu đô la, bao gồm lợi nhuận ròng 4,01 triệu đô la được tạo ra từ 1,09 triệu sản phẩm đã bán, cho thấy chuỗi cửa hàng đồ chơi này có tỷ suất lợi nhuận dương.
- 5 sản phẩm mang lại lợi nhuận cao nhất là: Colorbuds, Acton Figure, Lego Bricks, Deck of Cards, Glass Marbels.
- Có một xu hướng chung trong số liệu bán hàng tháng 2 và tháng 8, đó là doanh số bán hàng thấp hơn so với các tháng cùng kỳ năm trước. Cần triển khai các chiến lược tiếp thị để thúc đẩy doanh số bán hàng trong giai đoạn này.
- Toys là mặt hàng có doanh thu cao nhất, tiếp theo là Arts & Crafts..
- Việc kinh doanh tại khu Downtown đang phát triển mạnh, trong khi kinh doanh Toys  Airport lại không được tốt.
=> Do đó, cần đưa ra quyết định về tương lai của các cửa hàng tại sân bay dựa trên dòng tiền thu được từ từng cửa hàng cụ thể.

