# Hybrid Recommendation System for E-commerce

Dự án xây dựng hệ thống gợi ý sản phẩm lai ( **Hybrid** ) kết hợp giữa hành vi người dùng và đặc tính sản phẩm, giải quyết bài toán dữ liệu thưa ( **Sparsity** ) cực cao trong thương mại điện tử.

## Tổng quan dự án

Dự án tập trung vào việc cá nhân hóa trải nghiệm mua sắm bằng cách gợi ý các sản phẩm phù hợp nhất cho khách hàng. Hệ thống sử dụng mô hình Hybrid kết hợp hai phương pháp phổ biến:

* **Content-based Filtering** : Phân tích đặc tính sản phẩm (Tên, Danh mục).
* **Collaborative Filtering** : Phân tích hành vi mua sắm tương đồng giữa các khách hàng.

## Đặc điểm dữ liệu

* **Quy mô** : ~51,000 bản ghi giao dịch từ SQL Server.
* **Sparsity (Độ thưa)** : **99.92%** (Thách thức lớn nhất của dự án).
* **Insights từ EDA** :
* Thu nhập và Độ tuổi hầu như không có sự tương quan (0.00).
* Tỷ lệ khách hàng quay lại thấp, đòi hỏi mô hình phải mạnh về khả năng gợi ý theo danh mục.

## Kỹ thuật & Thuật toán

1. **Xử lý dữ liệu (Feature Engineering)** :

* **NLP** : Sử dụng `TF-IDF` để vector hóa tên sản phẩm.
* **Encoding** : `One-Hot Encoding` cho Category và Subcategory.
* **Scaling** : `MinMaxScaler` để chuẩn hóa điểm số trước khi kết hợp.

1. **Mô hình hóa (Modeling)** :

* **SVD (Singular Value Decomposition)** : Phân rã ma trận để trích xuất 50 yếu tố ẩn (latent factors).
* **Cosine Similarity** : Tính toán độ tương đồng giữa các vector sản phẩm.
* **Weighted Hybrid** : Kết hợp điểm số với trọng số **$\alpha=0.4$** cho Content-based.

## Kết quả đạt được

* **Category Precision Rate** : **66.****77%** (Độ chính xác dự báo danh mục sản phẩm).
* Hệ thống xử lý tốt lỗi **Cold Start** cho Item nhờ nhánh Content-based.
* Quy trình Evaluation chặt chẽ: Sử dụng Random Split để đảm bảo tính khách quan và ý nghĩa thống kê.

## Cấu trúc thư mục

**Plaintext**

```
├── .env                  		 # Thông tin cấu hình database (không upload)
├── hybrid_recommendation_system.ipynb   # File source code chính
├── README.md             		 # Hướng dẫn dự án
└── requirements.txt      		 # Các thư viện cần thiết
```

## Hướng dẫn cài đặt

1. Clone dự án:
   **Bash**

   ```
   git clone https://github.com/username/hybrid-recommender.git
   ```
2. Cài đặt thư viện:
   **Bash**

   ```
   pip install -r requirements.txt
   ```
3. Cấu hình file `.env` với các thông tin `server_name`, `db_name`, `username`, `password`
