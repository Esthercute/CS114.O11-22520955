# CS114.O11-22520955
Bài tập môn Machine Learning

Tên đề tài: Dự đoán hành vi mua hàng của khách hàng mua online 
1. Mô tả bài toán 
input: thông tin hóa đơn mua hàng của khách hàng mua online 
output: dự đoán hành vi mua hàng của khách hàng đó trong 90 ngày sau kể từ lần cuối thanh toán
mục tiêu: dự đoán hành vi khách hàng để có những chiến lược kinh doanh phù hợp
2. Mô tả về bộ dữ liệu
Nguồn: https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci/data
Số lượng: 1,067,371 hàng, 8 cột
Ngày: 1/12/2009 - 09/12/2011
Tiền xử lý dữ liệu: kiểm tra các features, loại bỏ các features không cần thiết khi chạy model, loại bỏ các giá trị null
Phân chia: train/test 8/2
3. Mô tả đặc trưng
data engineering: loại bỏ các features không cần thiết (...), thêm vào các features cần thiết (...)
data pipeline: load file csv từ nguồn, tiền xử lý dữ liệu và làm sạch, phân tích và đánh giá dữ liệu ban đầu, data engineering, dùng K-means phân cụm khách hàng, sau đó dán label cho các cụm,dùng các model predict hành vi của các loại khách hàng, đánh giá chung về xu hướng hành vi của khách hàng
4. Mô tả về thuật toán máy học
K-means để phân loại khách hàng 
chạy các loại model để chọn ra model phù hợp nhất
=> XGBClassifier để dự đoán hành vi của các loại khách hàng 
5. Cài đặt, tinh chỉnh tham số
6. Đánh giá và kết luận
