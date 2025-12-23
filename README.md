# 📊 YouTube Sentiment Insights: End-to-End MLOps Pipeline

[![MLOps: DVC](https://img.shields.io/badge/MLOps-DVC-red.svg)](https://dvc.org/)
[![MLOps: MLflow](https://img.shields.io/badge/Tracking-MLflow-blue.svg)](https://mlflow.org/)
[![Deployment: Docker](https://img.shields.io/badge/Deployment-Docker-blue.svg)](https://www.docker.com/)
[![Cloud: AWS](https://img.shields.io/badge/Cloud-AWS-orange.svg)](https://aws.amazon.com/)

Dự án xây dựng hệ thống phân tích cảm xúc bình luận YouTube theo thời gian thực. Hệ thống áp dụng quy trình MLOps hoàn chỉnh từ khâu thu thập dữ liệu, huấn luyện mô hình, quản lý phiên bản đến triển khai CI/CD trên hạ tầng AWS.



## 🌟 Key Features
- **Data Pipeline**: Quản lý bởi **DVC**, đảm bảo dữ liệu thô và tiền xử lý được phiên bản hóa chặt chẽ.
- **Experiment Tracking**: Sử dụng **MLflow** để theo dõi các tham số huấn luyện và quản lý Model Registry.
- **CI/CD Pipeline**: Tự động hóa quá trình đóng gói **Docker** và deploy lên **AWS EC2** thông qua **GitHub Actions**.
- **Cloud Infrastructure**: Lưu trữ dữ liệu trên **AWS S3** và phục vụ inference trên EC2.
- **User Interface**: Tích hợp dưới dạng **Chrome Extension**, cho phép người dùng xem phân tích cảm xúc ngay khi đang xem video.

## 🏗️ System Architecture
Hệ thống được thiết kế theo mô hình Modular:
1. **Data Ingestion**: Thu thập bình luận qua YouTube Data API.
2. **Preprocessing**: Làm sạch dữ liệu và trích xuất đặc trưng.
3. **Model Training**: Huấn luyện mô hình Sentiment Analysis (BERT/LSTM).
4. **API Service**: FastAPI cung cấp endpoint cho Chrome Extension.



## 🚀 Getting Started

### 1. Environment Setup
```bash
conda create -n youtube python=3.11 -y
conda activate youtube
pip install -r requirements.txt
```

### 2. DVC Pipeline
Để chạy lại toàn bộ quy trình xử lý và huấn luyện:
```bash
dvc init
dvc repro
```

Xem sơ đồ phụ thuộc của pipeline:
```bash
dvc 
```

### 3. AWS Configuration
Dự án sử dụng AWS S3 làm Remote Storage cho DVC và EC2 để deploy:
```bash
aws configure 
```

### 4. 🛠️ CI/CD Workflow
Mỗi khi có code mới được push lên nhánh main:

A. Linting & Testing: Kiểm tra chất lượng code.
B. Docker Build: Tự động build image mới.
C. Push to Registry: Đẩy image lên Docker Hub hoặc AWS ECR.
D. Auto Deploy: Cập nhật container mới trên AWS EC2.

bash
```
├── .dvc/                # Cấu hình quản lý phiên bản dữ liệu của DVC
├── .github/workflows/   # CI/CD pipeline (Tự động build Docker & deploy AWS)
├── flask_api/           # Backend API phục vụ inference cho Chrome Extension
├── notebooks/           # Jupyter Notebooks phục vụ EDA và thử nghiệm mẫu
├── src/                 # Mã nguồn chính của dự án
│   ├── data/            # Quản lý vòng đời dữ liệu
│   │   ├── data_ingestion.py # Thu thập dữ liệu từ YouTube API
│   │   ├── data_preprocessing.py# Kiểm tra chất lượng dữ liệu đầu vào
│   └── model/           # Quản lý huấn luyện và định danh mô hình
│       ├── model_building.py   # Script huấn luyện
│       ├── model_evaluation.py# Tính toán metrics (Accuracy, F1-score)
│       └── register_model.py # Đăng ký mô hình tốt nhất vào MLflow Model Registry
├── yt-chrome-plugin-frontend/ # Giao diện Chrome Extension (JavaScript/HTML/CSS)
├── Dockerfile           # Đóng gói ứng dụng thành Container
├── dvc.yaml             # Định nghĩa các giai đoạn (stages) của Pipeline
├── requirements.txt     # Danh sách thư viện cần thiết
└── setup.py             # Cài đặt project dưới dạng một package
```

📝 Acknowledge
Dự án được truyền cảm hứng và tham khảo quy trình triển khai từ cộng đồng MLOps (với các kỹ thuật từ entbappy).
