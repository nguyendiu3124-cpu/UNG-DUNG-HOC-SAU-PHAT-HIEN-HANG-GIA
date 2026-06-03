# Ứng dụng học sâu phát hiện hàng giả qua hình ảnh

## 1. Giới thiệu dự án

Dự án này xây dựng mô hình học sâu nhằm phân biệt sản phẩm **hàng thật** và **hàng giả** thông qua dữ liệu hình ảnh. Bài toán được triển khai theo hướng phân loại ảnh nhị phân, trong đó mỗi ảnh được gán một trong hai nhãn: `real` hoặc `fake`.

Mục tiêu của dự án là ứng dụng các mô hình thị giác máy tính hiện đại để hỗ trợ nhận diện hàng giả, từ đó góp phần nâng cao khả năng kiểm tra sản phẩm trong thương mại điện tử, bán lẻ và quản lý thị trường.

## 2. Mục tiêu nghiên cứu

Dự án tập trung vào các mục tiêu chính:

- Thu thập và xử lý dữ liệu hình ảnh sản phẩm thật và giả.
- Xây dựng bộ dữ liệu phân loại gồm hai nhóm: `real` và `fake`.
- Huấn luyện và đánh giá các mô hình học sâu dùng cho bài toán phân loại ảnh.
- So sánh hiệu quả của nhiều kiến trúc mô hình khác nhau.
- Đề xuất mô hình phù hợp nhất cho bài toán phát hiện hàng giả qua hình ảnh.

## 3. Dữ liệu sử dụng

Bộ dữ liệu gồm các hình ảnh sản phẩm (nguồn: Roboflow Universe) được chia thành hai nhãn:

- `real`: sản phẩm thật
- `fake`: sản phẩm giả

Sau quá trình gom và chuẩn hóa dữ liệu, tập dữ liệu có tổng cộng **1.961 ảnh**, bao gồm:

| Nhãn | Số lượng ảnh |
|---|---:|
| Real | 1.286 |
| Fake | 675 |

Dữ liệu được xử lý trên Google Colab, bao gồm các bước:

1. Kết nối Google Drive.
2. Giải nén dữ liệu ảnh từ file `.zip`.
3. Gom dữ liệu từ các thư mục `train`, `test`, `valid`.
4. Chuẩn hóa cấu trúc thư mục ảnh.
5. Tạo DataFrame gồm đường dẫn ảnh và nhãn tương ứng.

## 4. Phương pháp thực hiện

Quy trình triển khai dự án gồm các bước chính:

### Bước 1: Chuẩn bị dữ liệu

Dữ liệu ảnh được giải nén, kiểm tra và gom về cùng một cấu trúc thư mục. Mỗi ảnh được lưu kèm nhãn tương ứng để phục vụ quá trình huấn luyện và đánh giá mô hình.

### Bước 2: Khám phá dữ liệu

Dự án thực hiện phân tích phân bố nhãn để kiểm tra mức độ cân bằng giữa hai nhóm ảnh thật và ảnh giả. Đây là bước quan trọng vì mất cân bằng dữ liệu có thể ảnh hưởng đến khả năng nhận diện hàng giả của mô hình.

### Bước 3: Xây dựng mô hình học sâu

Ba mô hình học sâu được sử dụng và so sánh gồm:

- **MobileNetV2**
- **ResNet50**
- **Vision Transformer**

Các mô hình này được lựa chọn vì đều là những kiến trúc phổ biến trong thị giác máy tính, có khả năng trích xuất đặc trưng hình ảnh tốt và phù hợp với bài toán phân loại ảnh.

### Bước 4: Đánh giá mô hình

Hiệu quả của các mô hình được đánh giá bằng nhiều chỉ số khác nhau, bao gồm:

- Accuracy
- Precision đối với lớp hàng giả
- Recall đối với lớp hàng giả
- F1-score đối với lớp hàng giả
- ROC-AUC
- PR-AUC
- KS Statistic
- G-mean

Việc sử dụng nhiều chỉ số giúp đánh giá mô hình toàn diện hơn, đặc biệt trong bối cảnh bài toán phát hiện hàng giả cần quan tâm nhiều đến khả năng nhận diện đúng sản phẩm giả.

## 5. Kết quả mô hình

Kết quả thực nghiệm cho thấy mô hình **Vision Transformer** đạt hiệu quả tốt nhất về độ chính xác tổng thể và khả năng nhận diện hàng giả.

| Mô hình | Accuracy | Precision Fake | Recall Fake | F1 Fake | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| Vision Transformer | 0.9153 | 0.8812 | 0.8725 | 0.8768 | 0.9731 | 0.9335 |
| MobileNetV2 | 0.8881 | 0.9600 | 0.7059 | 0.8136 | 0.9823 | 0.9571 |
| ResNet50 | 0.6915 | 0.7037 | 0.1863 | 0.2946 | 0.6663 | 0.5518 |

Trong đó, **Vision Transformer** có Accuracy đạt khoảng **91,53%** và F1-score đối với lớp hàng giả đạt khoảng **87,68%**, cho thấy mô hình có khả năng cân bằng tốt giữa phát hiện đúng hàng giả và hạn chế nhầm lẫn.

## 6. Công nghệ sử dụng

Dự án được thực hiện bằng Python trên môi trường Google Colab, sử dụng các thư viện phổ biến trong xử lý dữ liệu và học sâu:

- Python
- Google Colab
- Pandas
- NumPy
- Matplotlib
- TensorFlow/Keras
- Scikit-learn
- MobileNetV2
- ResNet50
- Vision Transformer

## 7. Ý nghĩa thực tiễn

Dự án có tính ứng dụng trong các lĩnh vực:

- Phát hiện hàng giả trong thương mại điện tử.
- Hỗ trợ kiểm định sản phẩm bằng hình ảnh.
- Hỗ trợ doanh nghiệp, nhà bán lẻ và người tiêu dùng nhận diện rủi ro hàng giả.
- Làm nền tảng cho các hệ thống kiểm tra sản phẩm tự động trong tương lai.

## 8. Hướng phát triển tiếp theo

Trong tương lai, dự án có thể được mở rộng theo các hướng:

- Bổ sung thêm dữ liệu từ nhiều thương hiệu và nhóm sản phẩm khác nhau.
- Cải thiện chất lượng dữ liệu và cân bằng số lượng ảnh giữa hai lớp.
- Áp dụng kỹ thuật tăng cường dữ liệu để cải thiện khả năng khái quát hóa.
- Tối ưu mô hình để triển khai trên ứng dụng web hoặc mobile.
- Kết hợp mô hình phân loại ảnh với hệ thống quét mã QR, barcode hoặc thông tin sản phẩm.

## 9. Kết luận

Dự án cho thấy tiềm năng của học sâu trong việc phát hiện hàng giả thông qua hình ảnh. Kết quả thực nghiệm chứng minh rằng các mô hình thị giác máy tính, đặc biệt là Vision Transformer, có thể hỗ trợ hiệu quả trong bài toán phân biệt hàng thật và hàng giả. Đây là hướng tiếp cận có ý nghĩa thực tiễn cao, đặc biệt trong bối cảnh hàng giả ngày càng phổ biến trên các nền tảng thương mại điện tử.
