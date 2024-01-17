![image](https://github.com/Esthercute/CS114.O11-22520955/assets/87257260/96a61d05-ef03-49fd-be83-7ae16c02ff56)

# ĐỒ ÁN CUỐI KÌ MÔN MÁY HỌC
## BÀI TOÁN DỰ  ĐOÁN HÀNH VI MUA HÀNG CỦA KHÁCH HÀNG

*Giảng viên hướng dẫn:*
- PGS.TS. Lê Đình Duy
- ThS. Phạm Nguyễn Trường An

*Người thực hiện:*
Nguyễn Anh Hải Ngọc – 22520955

## I. Mô tả bài toán
- **Input:** Thông tin hóa đơn mua hàng của khách hàng.
- **Output:** Dự đoán hành vi mua hàng của khách hàng đó trong 90 ngày sau kể từ lần cuối thanh toán
- **Mục tiêu:** Giúp xác định những khách hàng nào mà team martketing cần tập trung vào đối với các chương trình khuyến mãi tiếp theo mà họ chuẩn bị triển khai.

## II. Mô tả về bộ dữ liệu
### Mô tả chung
- Nguồn: https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci/
- Số lượng: 1,067,371 hàng, 8 cột
- Mô tả:

| Tên cột      | Mô tả     |
|--------------|-----------|
| InvoiceNo | Số hóa đơn gồm 6 số      |
| StockCode      |  Mã sản phẩm  |
| Description      | Tên sản phẩm  |
| Quantity      |  Số lượng sản phẩm trong hóa đơn  |
| UnitPrice      | Đơn giá  |
| InvoiceDate      | Ngày mua hàng (trong khoảng từ 1/12/2009 – 9/12/2011)  |
| CustomerID      | Mã khách hàng (mỗi khách hàng sẽ có 1 mã riêng biệt không trùng nhau) |
| Country    | Tên đất nước của khách hàng mua hàng |

### Cách thức xây dựng bộ dữ liệu
#### Phân chia dữ liệu
Ta chia dữ liệu thành hai phần:
- Dữ liệu hành vi mua hàng của khách hàng, tính theo những đơn hàng có ngày mua hàng trong khoảng từ 1/12/2009 đến 30/08/2011
- Dữ liệu lần mua hàng đầu tiên tiếp theo, tính theo những đơn hàng có ngày mua hàng trong khoảng từ 1/9/2011 – 30/11/2011
-> Mục tiêu: sử dụng dữ liệu hành vi để dự đoán ngày mua hàng đầu tiên của khách hàng trong ba tháng tới. Nếu không có mua thì cũng dự đoán luôn.

#### Xử lý dữ liệu

![image](https://github.com/Esthercute/CS114.O11-22520955/assets/87257260/1620ac40-1e40-482f-b5ff-509efa24d57f)
- Xét dataset ta thấy có nhiều giá trị null, nên bước đầu ta xóa các giá trị null trong dataset đi.
- Xét cột InvoiceDate là cột ngày mua hàng nhưng lại có kiểu dữ liệu object, nên ta chuyển đổi nó sang kiểu datetime64

#### Xây dựng dữ liệu để xây dựng mô hình
- Tạo ra một dataframe mới cusID với thông tin mã khách hàng
- Từ bộ dữ liệu hành vi mua hàng của khách hàng, lấy ra những đơn hàng giao dịch cuối cùng của mỗi khách hàng.
- Từ bộ dữ liệu lần mua hàng đầu tiên tiếp theo, lấy ra những đơn hàng giao dịch đầu tiên của mỗi khách hàng.
- Tạo ra cột NextPurchaseDay trong cusID là số ngày kể từ lần mua hàng cuối hàng trong dữ liệu hành vi. Nếu có giá trị null thì gán cho giá trị 9999 để đồng bộ.

## III. Mô tả đặc trưng
### 1. Data engineering
Để xây dựng mô hình, em sẽ dùng hệ thống RFM score trong kinh tế học.
RFM score sẽ bao gồm các features:
-	Recency: thời gian mua hàng gần nhất
-	Frequency: tần suất mua hàng
-	Monetary: giá trị tiền mỗi lần mua hàng
Dùng unsupervised learning để phân cụm khách hàng và cho điểm giá trị của khách hàng theo từng feature.

### 2. Data pipeline
- Load và tiền xử lý dữ liệu
- Chia dữ liệu thành hai phần để tính chuẩn bị cho bước data engineering và build model
- Khởi tạo ra một dataframe mới từ dataset để chuẩn bị cho chạy model
- Dùng K-means để phân cụm khách hàng, sau đó đánh giá điểm số cho từng cụm
- Dùng các điểm số để dự đoán hành vi mua hàng tiếp theo của các khách hàng

## IV. Mô tả thuật toán máy học
- Sử dụng K-means để phân cụm và “chấm điểm” các hành vi của khách hàng
- Sử dụng các thuật toán Logistic Regression, GaussianNB, Random Forest Classifier, Deisio Tree Classifier, XGB Classifier, K-Neighbors Classifier để chạy và sử dụng thuật toán có accuracy cao nhất để cải tiến và đánh giá.

## V. Đánh giá kết quả và kết luận
Sau khi chạy một số thuật toán, thì ta thấy các accuracy chạy trên training set và test set đều trên 80%.
![image](https://github.com/Esthercute/CS114.O11-22520955/assets/87257260/9c8e331c-5691-45c2-8d42-b381b9378be0)

Sau đó, khi cải tiến thuật toán XGB Classifier thì accuracy đã tăng lên 90% cho training test và 88% cho test set.
![image](https://github.com/Esthercute/CS114.O11-22520955/assets/87257260/b7ad04ed-01c8-4e5a-bb14-6718ffe09f0f)

Ta có thể dùng mô hình này để dự đoán hành vi tiếp theo của các khách hàng trong những ngày tiếp theo.

Team marketing và business analyst của công ty có thể dùng những kết quả đó để dự đón nhu cầu thị trường cũng như hành vi của khách hàng để đưa ra những giải pháp và chương trình khuyến mãi phù hợp cho việc phát triển doanh thu.
