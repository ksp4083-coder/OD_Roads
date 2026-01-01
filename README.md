# Driving Object Detection Using YOLOv8

## 1. Dataset
- 공모전에 참가하여 수집한 한국교통안전공단 ['자율주행 공개데이터셋'](https://challenge.gcontest.co.kr/template/m/frame/downloadlist/16335?q=1368)
- 이미지 - 100,000장
- 가공 데이터 - 100,000장
- 데이터 구성 비율
  - training : validation : test = 8 : 1 : 1 <br>
  <p align="center">
  <img width="153.6" height="237.6" alt="image" src="https://github.com/user-attachments/assets/a0ae578e-50ec-4ebf-ad59-5907ede22929" />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <img width="128.4" height="232.8" alt="image" src="https://github.com/user-attachments/assets/44769e53-d3fd-4ef6-ab44-2203954dc7aa" />
  </p>
- json 파일 내용 설명 <br>
  <p align="center">
  <img width="594" height="187.8" alt="image" src="https://github.com/user-attachments/assets/9e9b4da5-d74c-4406-a31c-176b8cda1cee" />
  </p><br>

## 2. Development Process
### 2.1. Data Preprocessing (데이터 전처리.ipynb)
- 객체 탐지 YOLOv8 모델 학습을 위한 데이터 전처리 과정
- 가공된 객체 위치 정보 Bounding Box 좌표를 0 ~ 1 사이로 정규화
- 정규화 식은 아래와 같으며 Python 코드로 구현 <br>

$$ \large
\begin{aligned}
x_{\text{norm}} = \frac{x_{\text{center}}}{W_{\text{img}}}, \quad y_{\text{norm}} = \frac{y_{\text{center}}}{H_{\text{img}}}, \quad w_{\text{norm}} = \frac{w_{\text{BBox}}}{W_{\text{img}}}, \quad h_{\text{norm}} = \frac{h_{\text{BBox}}}{H_{\text{img}}}
\end{aligned}
$$
<br><br>

### 2-2. Model Selection & Optimization

본 프로젝트에서는 최적의 탐지 성능을 확보하기 위해 YOLOv8의 모든 모델 라인업(n, s, m, l, x)을 대상으로 비교 실험을 수행하였습니다. <br>

#### Model Comparison & Selection
- **실험 환경**: 동일한 학습 파라미터 및 하드웨어 환경에서 수행
- **평가 지표**: $mAP_{50}$ (mAP at IoU=0.5)
- **실험 결과**: 5가지 모델 중 **YOLOv8x (Extra Large)** 모델이 가장 높은 정확도를 기록하여 최종 모델로 선정되었습니다.

<div align="center">
  
| 모델 | 에폭 | 배치 크기 | 학습 시간 | 모델 구조 | mAP_{50} |
| :--: | :--: | :------: | :-------: | :-------: | :-----:
| YOLOv8n | 100 | 64 | 21.67 hours | 225 layers, 3,012,798 parameters | 0.71 |
| YOLOv8s | 100 | 64 | 22.23 hours | 225 layers, 11,139,470 parameters | 0.821 |
| YOLOv8m | 100 | 64 | 23.34 hours | 295 layers, 25,862,110 parameters | 0.866 |
| YOLOv8l | 100 | 64 | 24.17 hours | 365 layers, 43,637,550 parameters | 0.888 |
| YOLOv8x | 100 | 64 | 28.61 hours | 365 layers, 68,162,238 parameters | 0.901 |
| yolov8x.pt | 620 | 64 | 약 7일 21시간 | 365 layers, 68,162,238 parameters | 0.933 |

</div>

<br>

### 2-6. 모델 시연 영상

- 개발한 최종 모델을 활용해 주간/야간 도로 주행 영상에서 객체 탐지 수행

- [주간](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e)

- [야간](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a)







 

