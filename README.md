# 📈 Ứng dụng Tối ưu hóa Danh mục Đầu tư Chứng khoán HOSE

Ứng dụng web được xây dựng trên nền tảng **Streamlit** giúp nhà đầu tư và nhà nghiên cứu phân tích, tối ưu hóa tỷ trọng danh mục đầu tư cổ phiếu Việt Nam (sàn HOSE). 

Ứng dụng hiện thực hóa phương pháp học sâu động **LSTM-GRU (Dynamic Portfolio Optimization)** từ nghiên cứu trong notebook `KLTN_Final - Final.ipynb` và so sánh trực quan với hai phương pháp phân bổ tài sản truyền thống là **Phân bổ đều (Equal Weight)** và **Phân bổ 80-20 dựa trên Sharpe Ratio**.

---

## 📂 Cấu trúc Dự án khi đẩy lên GitHub

Để triển khai ứng dụng này lên Streamlit Cloud hoặc chia sẻ trên GitHub, bạn cần đẩy các file sau lên repository:

```text
├── app.py                      # File mã nguồn chính chạy Streamlit
├── requirements.txt            # Danh sách các thư viện Python cần thiết
├── README.md                   # Hướng dẫn sử dụng và triển khai (file này)
└── HOSE_2020_2023 (2).csv      # Dữ liệu giá lịch sử của các cổ phiếu (tùy chọn đẩy lên hoặc upload trực tiếp)
```

---

## 🛠️ Hướng dẫn Cài đặt & Chạy dưới Máy cục bộ (Local)

Làm theo các bước sau để thiết lập môi trường và khởi chạy ứng dụng trên máy tính của bạn:

### Bước 1: Tạo môi trường ảo (Khuyên dùng)
Mở Terminal (hoặc Command Prompt) tại thư mục dự án và chạy các lệnh sau:

* **Trên macOS / Linux:**
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```
* **Trên Windows:**
  ```cmd
  python -m venv venv
  venv\Scripts\activate
  ```

### Bước 2: Cài đặt các thư viện cần thiết
Cài đặt tất cả các thư viện phụ thuộc được liệt kê trong `requirements.txt`:
```bash
pip install -r requirements.txt
```

### Bước 3: Chạy ứng dụng Streamlit
Chạy lệnh sau để khởi chạy ứng dụng web:
```bash
streamlit run app.py
```
Sau khi chạy, trình duyệt web sẽ tự động mở giao diện ứng dụng tại địa chỉ mặc định: `http://localhost:8501`.

---

## 🚀 Hướng dẫn Triển khai (Deploy) lên Streamlit Cloud (Miễn phí)

Nền tảng Streamlit Cloud cho phép bạn deploy ứng dụng web của mình trực tiếp từ kho lưu trữ GitHub chỉ với vài cú click chuột:

### Bước 1: Đẩy code lên GitHub
1. Tạo một repository mới trên GitHub (ở chế độ Công khai - Public hoặc Riêng tư - Private).
2. Commit và push các file `app.py`, `requirements.txt` và `README.md` lên repository đó.
*(Lưu ý: Nếu file dữ liệu CSV nhỏ hơn 100MB, bạn có thể đẩy lên cùng repository, hoặc sử dụng tính năng tải file CSV trực tiếp từ giao diện ứng dụng).*

### Bước 2: Kết nối và Deploy trên Streamlit Cloud
1. Truy cập trang web [Streamlit Community Cloud](https://share.streamlit.io/) và đăng nhập bằng tài khoản GitHub của bạn.
2. Nhấn nút **Create App** (hoặc **New App**) ở góc trên bên phải.
3. Điền thông tin ứng dụng:
   - **Repository**: Chọn đường dẫn repository GitHub bạn vừa tạo.
   - **Branch**: Chọn branch chính (thường là `main` hoặc `master`).
   - **Main file path**: Điền `app.py`.
4. Nhấn nút **Deploy!**.

Hệ thống Streamlit Cloud sẽ tự động cài đặt môi trường từ `requirements.txt` và khởi chạy ứng dụng trong vòng 2-5 phút. Link ứng dụng của bạn sẽ có định dạng `https://<your-app-name>.streamlit.app/`.

---

## 💡 Các Tính năng chính của Ứng dụng

1. **Tổng quan Dữ liệu (Data Overview):**
   - Đọc dữ liệu tự động từ file CSV local hoặc file tải lên.
   - Lọc và hiển thị biểu đồ giá đóng cửa đã được chuẩn hóa để dễ quan sát xu hướng.
   - Tính toán nhanh Sharpe Ratio lịch sử và thống kê mô tả cho từng mã.
2. **Chiến lược Phân bổ Tĩnh (Static Allocation):**
   - **Phân bổ Đều (Equal Weight):** Chia đều tỷ trọng cho các mã có Sharpe tốt nhất.
   - **Phân bổ 80-20 theo Sharpe:** Top 20% số mã tốt nhất chiếm 80% vốn đầu tư và ngược lại.
   - Minh họa trực quan bằng **Treemap** và **Bar Chart**.
3. **Mô hình LSTM-GRU (Dynamic Model):**
   - Huấn luyện mô hình học sâu kết hợp trực tiếp trên giao diện.
   - Hỗ trợ chạy **Đa Seed (Multi-seed)** chọn ra mô hình tối ưu nhất để tránh bias như trong notebook.
   - Hiển thị lịch sử training loss và quá trình biến động tỷ trọng các tài sản theo thời gian.
4. **So sánh Hiệu quả (Comparison):**
   - Kiểm định chéo hiệu quả của 3 chiến lược trên **Tập Test** độc lập.
   - Biểu đồ **2 trục tích hợp (Dual-Axis Chart)** hiển thị Lợi nhuận, Rủi ro (Độ lệch chuẩn) và Sharpe Ratio.
   - Cho phép tải kết quả phân bổ tỷ trọng tối ưu dưới dạng file `.csv` để sử dụng thực tế.

---
*Phát triển bởi chuyên gia AI và kỹ sư Tài chính.*
