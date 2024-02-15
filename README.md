## ♻️ 서울시 스마트 수거함 입지 선정

**2023 Seoul Bigdata Campus Competition**

- **주제** : 순환경제 활성화를 위한 서울시 스마트 수거함 입지 선정

- **주제 선정 배경** : 순환경제 활성화 필요성, 폐플라스틱 수급 불안정, 스마트 수거함 현황 및 확대 필요성
- **필요성** : 순환경제 추진 정책 기여, 스마트 수거함 인식 변화와 참여 유도, 폐플라스틱 산업 경쟁 완화

- **기대효과** : 플라스틱 재활용률 증가, 환경보호를 위한 자원 효율성 증가, 재활용 프로세스 품질 향상
- **우선 입지 선정 결과** : 강서구 화곡 1동, 후보지 5곳 선정



### Requirements

<img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"><img src="https://img.shields.io/badge/Numpy-013243?style=for-the-badge&logo=numpy&logoColor=white"><img src="https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white"><img src="https://img.shields.io/badge/scikitlearn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white"><img src="https://img.shields.io/badge/matplotlib-150458?style=for-the-badge&logo=matplotlib&logoColor=white"><img src="https://img.shields.io/badge/seaborn-DD0700?style=for-the-badge&logo=seaborn&logoColor=white"><img src="https://img.shields.io/badge/Polygon-7B3FE4?style=for-the-badge&logo=polygon&logoColor=white"><img src="https://img.shields.io/badge/qgis-589632?style=for-the-badge&logo=qgis&logoColor=white"><img src="https://img.shields.io/badge/folium-77B829?style=for-the-badge&logo=folium&logoColor=white">



### 분석 프로세스

<img width="1133" alt="분석순서도" src="https://github.com/sin09135/Smart_Recycler_Location_Assessment/assets/139515794/588d118f-0eb3-4883-a00b-ca004048ede5">

---

### 1. 데이터 수집 및 전처리

- 개괄 : 2021년 데이터 기준 데이터 전처리 진행

- 사용 데이터 

  - 인구 : 2021 행정동 단위 거주인구 데이터, 2021 서울시 집계구 단위 내외국인 생활인구, 서울시 가구원 수 별 가구수 (동 별) 통계
  - 행정동 : 2021 전국 행정동 법정동 데이터
  - 위생업소 : 2019 서울시 식품위생업소 및 공중위생업소 데이터
  - 공간 : 2020 서울시 상주인구 공간데이터, 2023 행정동 해정경계 전자지도, 2016 서울시 10m 단위 도로구간 공간데이터, 생활밀접시설 위치 데이터
  - 재활용 : 2023 스마트 수거함 위치 데이터(직접수집) , 2021 구별 페트병 배출량

  

#### 2. 행정동 PET병 배출량 도출

- 분석 방법 : 다중회귀분석

- 분석 절차

  - 파생변수 생성

    - 상관계수(히트맵) 확인, 높은 상관관계(0.7)를 가진 변수를 중심으로 파생변수 생성

  - 다중공선성 확인

    - pearson 상관계수, VIF 확인

  - 예측 모델용 최종 변수 선정

    - 주요 경제활동 생활인구수, 1인가구 수 선정

  - 모델 생성 및 학습(자치구 데이터)

    - 최소제곱법(OLS) 기반 회귀 모델
    - 평가지표 : RMSE, MAE

  - 생성된 모델에 행정동 데이터 투입, 예측

<img width="1155" alt="변수 선택 및 모델 학습" src="https://github.com/sin09135/Smart_Recycler_Location_Assessment/assets/139515794/d66460d2-4010-411d-8cb3-4784e51026d0">


#### 3. 행정동 클러스터링

- 분석 방법 : kmeans clustering

- 분석 결과 : 군집 1(생활인구, 1인가구수, 수거함당 거주인구 높은 군집) 선정

<img width="1155" alt="클러스터링결과" src="https://github.com/sin09135/Smart_Recycler_Location_Assessment/assets/139515794/deb52420-8c41-4e71-92af-0fce87eeabf8">


#### 4. 행정동 PCA 입지 지수

- 분석 절차

  - 다중공선성 제거 : VIF 10 이하

  - Feature Selection 

    - Best Subset Selection, AIC 고려

  - PCA 입지 지수 개발

  - 입지 지수 적용

<img width="1159" alt="입지 지수" src="https://github.com/sin09135/Smart_Recycler_Location_Assessment/assets/139515794/a0114309-f46a-4787-a1e6-27792d885ec9">

#### 5. 행정동 내 스마트 수거함 입지 선정

- 분석 절차

  - 1. 입지 후보지 포인트 선정 , 도로 폭 5 이상 후보지 선택 ,근접 후보지 제거
    2. 입지 포인트 순위 선정
    3. 최종 입지 선정

<img width="1131" alt="최종입지선정" src="https://github.com/sin09135/Smart_Recycler_Location_Assessment/assets/139515794/08dea30b-a77d-46d8-ace4-061632e2d361">
