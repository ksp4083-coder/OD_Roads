# YOLOv8을 활용한 도로 주행 객체 탐지

## 1. 사용한 데이터
- 공모전에 참가하여 수집한 한국교통안전공단 ['자율주행 공개데이터셋'](https://challenge.gcontest.co.kr/template/m/frame/downloadlist/16335?q=1368)(40.9GB)
- 10만장의 이미지와 10종의 객체 위치 정보가 저장된 10만개의 json 파일 <br><br>
  <img width="128" height="198" alt="image" src="https://github.com/user-attachments/assets/a0ae578e-50ec-4ebf-ad59-5907ede22929" />
| 모델 | 에폭 | 배치 크기 | 학습 시간 | 모델 구조 | mAP@50 |
| :--: | :--: | :------: | :-------: | :-------: | :-----:
| yolov8n.pt | 100 | 64 | 21.67 hours | 225 layers, 3,012,798 parameters | 0.71 |
| yolov8s.pt | 100 | 64 | 22.23 hours | 225 layers, 11,139,470 parameters | 0.821 |
| yolov8m.pt | 100 | 64 | 23.34 hours | 295 layers, 25,862,110 parameters | 0.866 |
| yolov8l.pt | 100 | 64 | 24.17 hours | 365 layers, 43,637,550 parameters | 0.888 |
| yolov8x.pt | 100 | 64 | 28.61 hours | 365 layers, 68,162,238 parameters | 0.901 |
| yolov8x.pt | 620 | 64 | 약 7일 21시간 | 365 layers, 68,162,238 parameters | 0.933 |


- json 파일 속성


  <img width="590" height="182" alt="Image" src="https://github.com/user-attachments/assets/69e214f6-9391-41f0-a44a-8d6c3b80aba1" />

<br>

## 2. Progress
### 2-1. Normarlization
- 데이터 전처리.ipynb
- COCO dataset에서 사전 학습 된 YOLO 모델을 불러와 객체 탐지 모델 학습을 위한 Bounding Box 값 변환 과정
- 값은 0 ~ 1 사이로 정규화
- 객체 위치 정보 파일 예)
<img width="333" height="432" alt="Image" src="https://github.com/user-attachments/assets/c8b47ed1-5f2b-4110-9e6b-4ad034b28de7" />

<br>
<br>

- 변환 결과 예)
<img width="247" height="130" alt="1" src="https://github.com/user-attachments/assets/e4e16ba8-8d67-4eb5-8e54-528da78cacb0" />

<br>
<br>

### 2-2. 모델 학습 및 검증
- **검증 결과** <br>

| 모델 | 에폭 | 배치 크기 | 학습 시간 | 모델 구조 | mAP@50 |
| :--: | :--: | :------: | :-------: | :-------: | :-----:
| yolov8n.pt | 100 | 64 | 21.67 hours | 225 layers, 3,012,798 parameters | 0.71 |
| yolov8s.pt | 100 | 64 | 22.23 hours | 225 layers, 11,139,470 parameters | 0.821 |
| yolov8m.pt | 100 | 64 | 23.34 hours | 295 layers, 25,862,110 parameters | 0.866 |
| yolov8l.pt | 100 | 64 | 24.17 hours | 365 layers, 43,637,550 parameters | 0.888 |
| yolov8x.pt | 100 | 64 | 28.61 hours | 365 layers, 68,162,238 parameters | 0.901 |
| yolov8x.pt | 620 | 64 | 약 7일 21시간 | 365 layers, 68,162,238 parameters | 0.933 |

<br>
<br>

### 2-6. 모델 시연 영상

- 개발한 최종 모델을 활용해 주간/야간 도로 주행 영상에서 객체 탐지 수행

- [주간](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e)

- [야간](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a)







 

