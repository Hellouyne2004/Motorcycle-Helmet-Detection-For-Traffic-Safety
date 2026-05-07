# 🏍️ Motorcycle Helmet Detection For Traffic Safety

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)
![YOLO11](https://img.shields.io/badge/YOLO11-00FFFF?style=for-the-badge&logo=YOLO&logoColor=black)
![EfficientNetV2](https://img.shields.io/badge/EfficientNetV2-4B8BBE?style=for-the-badge)
![Kaggle](https://img.shields.io/badge/Kaggle-035a7d?style=for-the-badge&logo=kaggle&logoColor=white)

Hệ thống nhận diện người đội mũ bảo hiểm khi tham gia giao thông bằng xe máy nhằm nâng cao an toàn đường bộ. Dự án đề xuất một giải pháp học sâu đa bước (multi-stage deep learning pipeline) kết hợp khả năng phát hiện vật thể, theo dõi thời gian thực và phân loại đa nhãn để xác định chính xác tình trạng đội mũ của từng người trên xe.

## 📖 Tổng quan (Abstract)
Phát hiện việc sử dụng mũ bảo hiểm là bài toán cốt lõi trong giao thông thông minh. Khắc phục hạn chế của các phương pháp nhận diện trên từng khung hình đơn lẻ, hệ thống của chúng tôi phối hợp 3 thành phần chính:
1. **Phát hiện (Motorcycle Detection)**: Sử dụng **YOLO11n** để định vị xe máy.
2. **Theo dõi đa đối tượng (Multi-Object Tracking)**: Áp dụng thuật toán **BoT-SORT** (kết hợp bộ lọc Kalman) để duy trì định danh xe xuyên suốt luồng video.
3. **Phân loại đa nhãn (Multi-label Classification)**: Sử dụng mạng **EfficientNetV2-S** với kiến trúc 6-node để xác định độc lập tình trạng đội mũ của từng vị trí: Người lái (Driver), Hành khách 1 (Passenger 1) và Hành khách phụ (Extra Riders).
4. **Cơ chế bỏ phiếu (CHUE Soft Voting)**: Áp dụng theo chuỗi thời gian của từng phương tiện giúp loại bỏ nhiễu do che khuất (occlusion).

## 🗂️ Dữ liệu (Dataset)
Dự án sử dụng bộ dữ liệu giám sát giao thông đã được tối ưu hóa:
- **Link Dataset**: [Helmet Dataset by OSF Lite (Kaggle)](https://www.kaggle.com/datasets/kronomy/helmet-dataset-by-osf-lite)

## 📂 Cấu trúc thư mục (Directory Structure)
Pipeline của hệ thống được chia thành các bước rõ ràng trong thư mục `src/`:

- `step2-trainyolo.ipynb`: Xử lý dữ liệu và huấn luyện mô hình YOLO11n để phát hiện người/xe máy.
- `step3-tracking.ipynb`: Khởi tạo và kiểm thử thuật toán BoT-SORT để theo dõi quỹ đạo phương tiện.
- `step4-data-train-efficientnet.ipynb`: Cắt dữ liệu (crop) từ các track và huấn luyện mạng EfficientNetV2-S với đầu ra 6 nút phân loại đa nhãn.
- `step5-combine.ipynb`: Tích hợp toàn bộ pipeline (YOLO11 + BoT-SORT + EfficientNetV2 + Soft Voting) lên video test.
- `step6-evaluate.ipynb`: Đánh giá hiệu năng và các độ đo (Metrics) của hệ thống.

## 🚀 Hướng dẫn cài đặt & Chạy (Usage)
1. Clone repository này về máy.
2. Cài đặt các thư viện cần thiết (có thể chạy trong môi trường Conda/Virtualenv):
   ```bash
   pip install ultralytics torch torchvision opencv-python pandas
   ```
3. Tải dataset từ Kaggle và đặt vào thư mục tương ứng.
4. Mở Jupyter Notebook / JupyterLab và chạy tuần tự từ `step2` đến `step6`.

## 👥 Nhóm Tác giả (Authors)
**Nhóm 12 - Giữa kỳ Computer Vision** (Trường Đại học Công nghiệp TP.HCM - IUH)
- Trương Long Tỷ
- Nguyễn Thái Uy
- Trần Anh Tuấn
