# Sinh mô tả ảnh (Image Captioning)

Notebook xây dựng một mô hình **Image Captioning** (tạo mô tả tự động cho ảnh) sử dụng kiến trúc **Encoder-Decoder** kết hợp với **InceptionV3**, **LSTM** và **Attention Mechanism**. Ngoài ra, có **Fine-tune bằng mô hình BLIP (Bootstrapping Language-Image Pretraining)** để so sánh và đánh giá chất lượng.

## Mục tiêu
Xây dựng hệ thống sinh mô tả tự động cho ảnh, có khả năng hiểu nội dung hình ảnh và mô tả bằng câu văn tự nhiên. Ứng dụng trong:

## Mô hình
### 1. Encoder - InceptionV3
- Trích xuất đặc trưng từ ảnh đầu vào
- Sử dụng mô hình đã huấn luyện trước trên ImageNet, loại bỏ tầng fully connected

### 2. Decoder - LSTM + Attention
- LSTM sinh mô tả tuần tự dựa trên đặc trưng ảnh
- Attention giúp mô hình tập trung vào các vùng ảnh tương ứng trong quá trình sinh từ

### 3. Fine-tune bằng BLIP
- Sử dụng BLIP từ thư viện HuggingFace để sinh mô tả tham chiếu và cải thiện kết quả

### Cấu trúc mô hình:

      [Input Image]
             |
             v
    +-------------------+
    |   InceptionV3     |   ← Encoder (trích đặc trưng)
    | (Pretrained CNN)  |
    +-------------------+
             |
             v
    [Image Features: vector 2048-d]
 
             |
             v
    +-------------------+        +-------------------------+
    |  Attention Layer  | <----- |  Image Features (context)|
    +-------------------+        +-------------------------+
             |
             v
    +-------------------+
    |  Embedding Layer  |
    +-------------------+
             |
             v
    +-------------------+
    |   LSTM Decoder    |   ← Decoder sinh caption
    +-------------------+
             |
             v
     [Generated Caption]

## Dữ liệu
### 1. Tập dữ liệu: **COCO 2017**
- Ảnh và mô tả được tiền xử lý, mã hóa, lưu tokenizer và đặc trưng ảnh

### 2. Tập dữ liệu: **Flickr30k**
- Ảnh và mô tả được tiền xử lý, mã hóa, lưu tokenizer và đặc trưng ảnh

## Công nghệ sử dụng
- Python, TensorFlow / Keras
- NumPy, Matplotlib, Pillow
- HuggingFace Transformers (BLIP)

## Kết quả
- Mô hình sinh mô tả tương đối sát nội dung ảnh
<img src="https://github.com/user-attachments/assets/db174b2b-cdbf-4962-aae5-a780171969b3" width="500"/>
<img src="https://github.com/user-attachments/assets/8be2a290-b6b5-4a00-930d-58b8ae937b49" width="500"/>
<img src="https://github.com/user-attachments/assets/67c668b5-386c-497d-920e-b65c0283da5c" width="500"/>
<img src="https://github.com/user-attachments/assets/c3995cd2-a428-44e0-a22d-f18544038c2c" width="500"/>

- BLIP giúp cải thiện chất lượng mô tả và kết quả được cải thiện rất nhiều



## Định hướng phát triển
- Huấn luyện mô hình với encoder tiên tiến hơn (ViT, Swin Transformer)
- Tích hợp giao diện người dùng với Flask / Streamlit

## Tác giả
**Lê Quang Tuấn** 
