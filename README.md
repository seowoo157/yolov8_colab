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
<b> 코드 설명하기
이 코드는 Google Colab에서 업로드한 이미지에 대해 YOLO(You Only Look Once) 모델을 사용하여 객체 탐지(Object Detection)를 수행하는 Python 스크립트입니다. 각 부분에 대해 설명하겠습니다:

### 1. **필요한 패키지 설치**:
```python
%pip install ultralytics opencv-python-headless matplotlib
```
- **`ultralytics`**: YOLOv8 모델을 포함한 패키지입니다.
- **`opencv-python-headless`**: GUI 없이 OpenCV를 사용할 수 있는 버전으로, Google Colab에서 이미지 처리를 할 때 유용합니다.
- **`matplotlib`**: 이미지나 그래프를 표시할 때 사용하는 라이브러리입니다.

### 2. **이미지 업로드**:
```python
from google.colab import files  

uploaded = files.upload() 
filename = next(iter(uploaded))    # 업로드된 파일 이름을 가져옵니다. 
```
- **`files.upload()`**: Google Colab에서 파일 업로드를 위한 함수로, 로컬에서 이미지를 Colab 환경으로 업로드합니다.
- **`filename = next(iter(uploaded))`**: 업로드된 파일 중 첫 번째 파일의 이름을 `filename` 변수에 저장합니다.

### 3. **디렉토리 생성 및 파일 이동**:
```python
!mkdir -p /content/sample_data  # 업로드된 파일을 저장할 디렉토리 생성
!mv {filename} /content/sample_data/{filename}
```
- **`!mkdir -p /content/sample_data`**: `sample_data`라는 디렉토리가 `/content` 안에 없으면 생성합니다.
- **`!mv {filename} /content/sample_data/{filename}`**: 업로드된 이미지를 `sample_data` 디렉토리로 이동합니다.

### 4. **YOLO 모델 로드**:
```python
from ultralytics import YOLO 
model = YOLO('yolov8n.pt')  # YOLO 모델 파일 로드
```
- **`from ultralytics import YOLO`**: YOLO 모델을 사용하기 위한 클래스를 `ultralytics` 패키지에서 가져옵니다.
- **`model = YOLO('yolov8n.pt')`**: 사전 훈련된 `yolov8n.pt` 모델 파일을 로드합니다. 이 파일은 객체 탐지를 위한 훈련된 모델입니다.

### 5. **이미지 경로 지정 및 예측 수행**:
```python
image_path = '/content/sample_data/1.jpg'  # 이미지 파일 경로
results = model.predict(image_path)  # 예측 결과를 저장
```
- **`image_path = '/content/sample_data/1.jpg'`**: 업로드한 이미지 파일의 경로를 지정합니다. 이 경로를 실제 업로드한 파일의 이름에 맞게 수정해야 할 수 있습니다.
- **`results = model.predict(image_path)`**: 지정한 이미지에서 객체 탐지를 수행하고, 그 결과를 `results` 리스트로 반환합니다. `results`는 탐지된 객체에 대한 정보가 담긴 객체 목록입니다.

### 6. **결과 이미지 저장**:
```python
first_result = results[0]  # 첫 번째 결과 객체를 가져옵니다.
first_result.save()  # 탐지된 객체가 표시된 이미지를 저장합니다.
```
- **`first_result = results[0]`**: `results` 리스트의 첫 번째 객체를 가져옵니다. 이 객체는 이미지에서 탐지된 객체에 대한 정보를 담고 있습니다.
- **`first_result.save()`**: 탐지된 객체들이 표시된 이미지를 저장합니다. 저장된 이미지는 원본 이미지에 객체 탐지 결과(바운딩 박스와 라벨)가 추가됩니다.

### 7. **결과 이미지 표시**:
```python
saved_image_path = '/content/results_1.jpg'  # 저장된 이미지 경로
display(Image(filename=saved_image_path))  # 이미지를 화면에 표시
```
- **`saved_image_path = '/content/results_1.jpg'`**: 탐지된 객체가 포함된 이미지를 저장한 경로를 지정합니다. 경로와 파일 이름을 필요에 맞게 수정할 수 있습니다.
- **`display(Image(filename=saved_image_path))`**: `saved_image_path`에서 저장된 이미지를 Google Colab에서 화면에 표시합니다.

### 요약:
이 코드는 다음과 같은 작업을 수행합니다:
1. 이미지를 업로드하여 Google Colab 환경에 저장합니다.
2. YOLO 모델을 사용하여 이미지에서 객체 탐지를 수행합니다.
3. 탐지된 객체가 표시된 이미지를 저장하고, 이를 화면에 표시합니다.

이 과정은 주로 객체 탐지 작업에서 사용할 수 있으며, 업로드한 이미지에서 사람, 동물, 차량 등 다양한 객체를 탐지하고 그 결과를 시각적으로 확인할 수 있습니다.

추가적인 질문이나 도움이 필요하시면 언제든지 말씀해 주세요!



![results_1 (1)](https://github.com/user-attachments/assets/21fe1741-94a4-48bb-a341-450730ffbf6f)

