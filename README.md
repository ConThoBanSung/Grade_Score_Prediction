# Dự đoán điểm số sinh viên bằng mô hình LSTM

## Giới thiệu
Dự án này sử dụng mô hình LSTM (Long Short-Term Memory) để dự đoán điểm số của sinh viên dựa trên dữ liệu đầu vào. Mô hình được huấn luyện bằng TensorFlow/Keras và đánh giá bằng các chỉ số như MAE, MSE, RMSE, và R2 Score.

## Yêu cầu hệ thống
- Python 3.x
- Thư viện:
  - `numpy`
  - `pandas`
  - `joblib`
  - `matplotlib`
  - `seaborn`
  - `scikit-learn`
  - `tensorflow`

Cài đặt các thư viện cần thiết bằng lệnh:
```sh
pip install numpy pandas joblib matplotlib seaborn scikit-learn tensorflow
```

## Các bước thực hiện

### 1. Chia dữ liệu thành tập train và test
- Đọc dữ liệu từ file `student_scores.csv`
- Chia dữ liệu thành đầu vào (`X`) và nhãn (`y`)
- Chuẩn hóa dữ liệu bằng `MinMaxScaler`
- Chia thành tập huấn luyện và kiểm tra với tỷ lệ 80-20

### 2. Định dạng dữ liệu cho LSTM
- Chuyển đổi dữ liệu thành dạng phù hợp với mô hình LSTM (3 chiều: samples, timesteps, features)

### 3. Xây dựng mô hình LSTM
- Mô hình có 2 lớp `LSTM` với kích thước 64 và 32
- Sử dụng `Dropout` để tránh overfitting
- Dùng `Dense` để tạo đầu ra
- Sử dụng `Adam` làm optimizer và `MSE` làm loss function

### 4. Huấn luyện mô hình
- Huấn luyện với `EarlyStopping` để dừng sớm nếu không có cải thiện
- Số epoch tối đa là 100, batch size là 16

### 5. Lưu mô hình và bộ chuẩn hóa
- Lưu mô hình đã train vào file `student_score_lstm.h5`
- Lưu scaler dùng cho chuẩn hóa vào `scaler_X.pkl` và `scaler_y.pkl`

### 6. Dự đoán
- Sử dụng mô hình để dự đoán điểm số sinh viên trên tập kiểm tra
- Chuyển đổi kết quả về giá trị ban đầu bằng `inverse_transform`

### 7. Đánh giá mô hình
- Sử dụng các chỉ số:
  - MAE (Mean Absolute Error)
  - MSE (Mean Squared Error)
  - RMSE (Root Mean Squared Error)
  - R2 Score

### 8. Trực quan hóa kết quả
- Vẽ biểu đồ thực tế vs dự đoán
- Biểu đồ phân phối sai số
- Biểu đồ hộp (boxplot) thể hiện sự phân tán lỗi

### 9. Kiểm tra mô hình với toàn bộ dữ liệu
- Tải lại mô hình đã lưu và dự đoán trên toàn bộ dataset
- Xuất kết quả thực tế và dự đoán thành DataFrame

## Hướng dẫn chạy chương trình
1. Chuẩn bị dữ liệu `student_scores.csv`
2. Chạy toàn bộ script để huấn luyện mô hình và lưu kết quả
3. Kiểm tra kết quả dự đoán và đánh giá mô hình

## Kết quả mẫu
Ví dụ kết quả đầu ra:
```
MAE: 2.45, MSE: 8.32, RMSE: 2.89, R2 Score: 0.85
```

## Tác giả
Nguyễn Huỳnh Hoàng Kha
