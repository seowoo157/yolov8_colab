# yolov8_colab
``` bash
# 필요한 패키지 설치
%pip install ultralytics opencv-python-headless matplotlib

# 파일 업로드를 위한 라이브러리 import
from google.colab import files  

# 이미지 파일 업로드
uploaded = files.upload() 
filename = next(iter(uploaded))    # 업로드된 파일 이름을 가져옵니다. 

# 업로드된 이미지 파일을 적절한 디렉토리로 이동 
!mkdir -p /content/sample_data  # 업로드된 파일을 저장할 디렉토리 생성
!mv {filename} /content/sample_data/{filename}

# YOLO 모델 로드
from ultralytics import YOLO 
from IPython.display import Image, display

# Load a pretrained YOLO model
model = YOLO('yolov8n.pt')  # Correct model file

# Define path to the image file 
image_path = '/content/sample_data/1.jpg'  # Correct path to the image

# Run inference on the image
results = model.predict(image_path)  # List of Result objects

# Assuming results[0] contains the desired Result object
first_result = results[0]

# Save the result image
first_result.save()  # This will save the image with detections

# Specify the path to the saved image
saved_image_path = '/content/results_1.jpg'  # Update this to where the image gets saved

# Display the saved image
display(Image(filename=saved_image_path))
```
![results_1 (1)](https://github.com/user-attachments/assets/21fe1741-94a4-48bb-a341-450730ffbf6f)
