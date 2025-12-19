# YOLO : 도로 주행 객체 탐지>

## 1. 사용 데이터셋
- 공모전에서 제공한 한국교통안전공단 ['자율주행 공개데이터셋'](https://challenge.gcontest.co.kr/template/m/frame/downloadlist/16335?q=1368)(40.9GB)
- 도로 주행 중 촬영된 10만장의 이미지와 각각의 이미지에 10종 객체의 위치 정보가 표기(라벨링)된 객체 위치 정보 json 파일
  - training : 80,000(.jpg), 80,000(.json)
  - validation : 10,000(.jpg), 10,000(.json) 

- json 파일 속성


  <img width="590" height="182" alt="Image" src="https://github.com/user-attachments/assets/69e214f6-9391-41f0-a44a-8d6c3b80aba1" />

<br>

## 2. 개발 과정
### 2-1. 객체 위치 정보 정규화
- COCO dataset에서 사전학습 된 YOLO 모델을 불러와 Custome 데이터셋을 학습시키기 위해 객체 위치 정보 Bounding Box 값을 YOLO 형식인 0 ~ 1 사이의 값으로 변환
- 객체 위치 정보 파일(.json) 구조 예시
<img width="333" height="432" alt="Image" src="https://github.com/user-attachments/assets/c8b47ed1-5f2b-4110-9e6b-4ad034b28de7" />

<br>
<br>

- 변환 결과 예시
<img width="247" height="130" alt="1" src="https://github.com/user-attachments/assets/e4e16ba8-8d67-4eb5-8e54-528da78cacb0" />

<br>
<br>

### 2. 모델 학습
<img width="659" height="152" alt="Image" src="https://github.com/user-attachments/assets/ccdf299f-6ac9-409e-ad97-67a14824e575" />

<br>
<br>

### 3. 최종 모델 학습
<img width="660" height="67" alt="Image" src="https://github.com/user-attachments/assets/968cfbeb-468d-4a30-9d99-bb9eaa671482" />

<br>
<br>

### 4. 시연 영상
- [test dataset](https://github.com/user-attachments/assets/715ef921-bc30-4d1c-8d89-b6caf0dff56a)

- [daytime](https://github.com/user-attachments/assets/1867900f-da03-4578-b419-428d62d5cc6e)

- [night](https://github.com/user-attachments/assets/45fd9091-5d0a-4dc5-b9da-cfb9ff2c104a)







 

