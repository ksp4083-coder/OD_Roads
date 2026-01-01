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
  </p>

<br>

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

<br>

### 2.2. Model Selection & Optimization

본 프로젝트에서는 도로 주행 환경에서 최적의 탐지 성능을 확보하기 위해 YOLOv8의 모든 모델 라인업(n, s, m, l, x)을 대상으로 성능 비교 실험을 수행하였습니다. 

<br>

### 2.3. Model Comparison & Selection
- **실험 환경**: 동일한 학습 파라미터 및 하드웨어 환경에서 수행
- **평가 지표**: $mAP_{50}$ (mAP at IoU=0.5)
- **실험 결과**: 5가지 모델 중 **YOLOv8x (Extra Large)** 모델이 가장 높은 정확도를 기록하여 최종 모델로 선정되었습니다.

<div align="center">
  
| Model Variant | Input Size | Params (M) | mAP50 (Base) |
| :--: | :--: | :------: | :-----:
| YOLOv8n | 640 | 3.01 | 0.71 |
| YOLOv8s | 640 | 11.14 | 0.821 |
| YOLOv8m | 640 | 25.86 | 0.866 |
| YOLOv8l | 640 | 43.64 | 0.888 |
| **YOLOv8x (Selected)** | **640** | **68.16** | **0.901** |

</div>

<br>

### 2.4. Intensive Training for Performance Boost
최종 선정된 **YOLOv8x** 모델의 탐지 성능을 극대화하기 위한 최적화 단계

<div align="center">

**[ Final Training  Configuration ]**

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Model Variant** | **YOLOv8x** | 가장 큰 모델 라인업 선택 |
| **Epochs** | **620** | 탐지 성능 극대화를 위한 추가 학습 |
| **Batch Size** | **64** | GPU 메모리(VRAM) 최적화 크기 |
| **Image Size** | **640 x 640** | 표준 입력 해상도 |
| **Optimizer** | **SGD** | Momentum: 0.937 적용 |
| **Learning Rate** | **0.01 (lr0)** | 초기 학습률 |
| **Total Training Time** | **약 7일 21시간** | 일주일 이상 학습 |
| **Hardware** | **NVIDIA A100 GPU** | DSC 공유대학 고성능 GPU 서버 활용 |
| **mAP50** | **0.933** | IoU = 0.5에서 mAP 값 |

<br>

**결과**: 추가 학습을 통해 $mAP_{50}$ 수치가 **0.901에서 0.933으로 약 3.2%p 향상**되었으며, 도로 주행 환경에서의 객체 탐지 성능 확보

</div>

<br>

### 2.5. Training Results Visualization
모델의 학습 과정 및 최종 성능을 시각화한 결과입니다.

<div align="center">

**[ Loss & mAP Curves ]**

<img width="622.5" height="299.5" alt="image" src="https://github.com/user-attachments/assets/9100d82f-2605-4877-9409-935de240d40c" />

> **Figure 1**: Epoch에 따른 Loss 감소 및 mAP 상승 추이 (최종 mAP@50: 0.933)

</div>

<br>

### 3. Inference Demonstration
- 개발한 최종 모델을 활용해 주간 및 야간 도로 주행 환경에서 실시간 객체 탐지 성능을 검증하였습니다.

<div align="center">

| 주간 주행 (Daytime) | 야간 주행 (Nighttime) |
| :---: | :---: |
| [▶ 영상 보기](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e) | [▶ 영상 보기](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a) |

**Figure 2**: Real-world inference testing in various lighting conditions.

</div>

- [주간](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e)

- [야간](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a)







 

