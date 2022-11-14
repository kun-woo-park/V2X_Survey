# Surveying on V2X

# About V2X

![그림 1. V2X 개요[1]](Surveying%20on%20V2X%202d641d291bca45f4b4bdddf0075b2628/Untitled.png)

그림 1. V2X 개요[1]

자율주행차량에 여러 센서 데이터들을 장착하더라도 실 도로에서의 주행에는 한계가 발생한다. 가파른 언덕을 주행하거나, 악천후에서의 주행과 같은 상황들에서는 차량 스스로의 센서데이터들 만으로는 주변 상황을 파악하기 어렵다. 

따라서 차세대 지능형 교통체계의 연구방향은 차량 주행 도중 차량과 주변 환경간의 유기적인 상호작용을 통해 교통정보를 교환하거나 공유하는 방향으로 연구가 진행되고 있고, 이처럼 차량과 주변 환경 사이의 통신기술을 총칭하여 V2X라고 한다[3].

![그림 2. V2X 포함 기술 개요 1[2]](Surveying%20on%20V2X%202d641d291bca45f4b4bdddf0075b2628/Untitled%201.png)

그림 2. V2X 포함 기술 개요 1[2]

V2X(Vehicle to Everything) 통신 기술이란 차량이 유,무선망을 통해 다른 차량 및 도로 등 인프라가 구축된 사물과 정보를 교환하는 것 또는 그 기술을 의미하며[4], V2V(Vehicle to Vehicle), V2I(Vehicle to Infrastructure)[5], V2P(Vehicle to Pedestrian), V2C(Vehicle to Cloud) 형태의 기술을 총칭 한다.

![그림 3. V2X 포함 기술 개요 2[2]](Surveying%20on%20V2X%202d641d291bca45f4b4bdddf0075b2628/Untitled%202.png)

그림 3. V2X 포함 기술 개요 2[2]

V2X는 현재 두개의 통신 표준이 대두되고 있으며[6], 이동통신 기반의 C-V2X(Cellular Vehicle to Everything)와 근거리 WiFi기반의 DSRC(Dedicated Short Range Communication) 이 그들이다.

## C-V2X와 DSRC기술 비교[7][8][9]

|  | C-V2X | DSRC |
| --- | --- | --- |
| 통신기술 | LTE, 5G 이동통신 기반 | WAVE 와이파이 기반 |
| 통신거리 | 수 km | 300m (1km 미만) |
| 통신 표준 | 3GPP Rel. 14, 15 | IEEE 802.11p |
| 장점 | 넓은 커버리지(서비스 가능 거리), 전송속도, 보안에 강 | 기존 인프라, 설비 활용가능
충분한 데이터로 안정적 |
| 단점 | 인프라 구축에 신규 투자비용 발생 | 좁은 커버리지, 보안에 취약 |
| 파일럿 테스트 | 네바다주 라스베가스 테스트발표(2019년) | 뉴욕, 플로리다 파일럿테스트 진행 |

본 프로젝트에서 사용하는 통신표준은 DSRC 방식의 WAVE(Wireless Access in Vehiclular Environment) 이며, 특징은 아래와 같다.

## Specification of Wave Communication[10][11]

| 주요 특징 | 내용 |
| --- | --- |
| 통신 대역폭 | 5.855 ~ 5.925 GHz |
| 채널 수 | 7개 |
| 채널 대역폭 | 10 MHz |
| 무선 지연 | 100ms 내외 |
| 최대 전송 속도 | 27 Mbps |
| 전송 범위 | 최대 1km |
| 지원 가능한 차량 이동속도 | 최대 200km/h |

# Implementation of V2X on Autonomous driving system[12][13][14][15][16]

V2X의 실질적인 서비스 예시는 아래의 그림과 같다.

![그림 4. 기본 V2X 서비스 1[17]](Surveying%20on%20V2X%202d641d291bca45f4b4bdddf0075b2628/Untitled%203.png)

그림 4. 기본 V2X 서비스 1[17]

![그림 5. 기본 V2X 서비스 2[17]](Surveying%20on%20V2X%202d641d291bca45f4b4bdddf0075b2628/Untitled%204.png)

그림 5. 기본 V2X 서비스 2[17]

![그림 6. V2I 서비스를 위해 인프라로부터 제공 받는 정보 개요[18]](Surveying%20on%20V2X%202d641d291bca45f4b4bdddf0075b2628/Untitled%205.png)

그림 6. V2I 서비스를 위해 인프라로부터 제공 받는 정보 개요[18]

아래는 발생 가능한 시나리오들을 정리한 것으로 화살표(→) 이후의 정보들은 주행 차량(Ego Vehicle)의 데이터 이외에 추가적으로 V2X로부터 제공 받아야 하는 데이터들을 의미한다. 

## For Perception[19]

- 악천후 상황에서의 주변 차량 인지 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V)
- 사각지대 위치의 객체(차량, 보행자 등) 인지 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V)
- 차량 간 위치정보 공유를 통한 인지 보정 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V)
- 차량 간 위치정보 공유를 통한 인지 labeling → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V)

## For Localization[20]

- 악천후 상황에서의 현재 차량 위치 측위 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception정보(V2V)
- 터널 진입 시 측위 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception정보(V2V)
- GNSS Jamming 시 측위 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception정보(V2V)

## For Prediction and Planning[21][22][23]

- 악천후 상황에서의 주변 차량 경로 예측 및 경로 계획 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception정보(V2V), 주변 차량의 IMU정보(V2V), 신호등 신호 정보(V2I)
- 사각지대 위치의 객체(차량, 보행자 등)에 대한 경로 예측 및 경로 계획 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V), 주변 차량의 IMU정보(V2V)
- 고장, 급정거 차량에 대한 경로예측 및 경로계획 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V), 주변 차량의 IMU정보(V2V), 고장 차량에 대한 교통상황 정보(V2I)
- 교차로 과속, 긴급차량에 대한 경로예측 및 경로계획 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V), 주변 차량의 IMU정보(V2V), 교통상황 정보(V2I)
- 차량 간 위치정보 및 물리정보 공유를 통한 경로 예측 보정 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception정보(V2V), 주변 차량의 IMU정보(V2V)
- 장애물(포트 홀, 불법주정차, 역주행, 보행자 등) 회피를 위한 경로 계획 → 장애물 위치 정보(V2I), 주변 차량의 GNSS정보(V2V), 주변 차량의 perception정보(V2V)
- 주행 효율 증대를 위한 군집 주행 경로 계획 → 주변 차량의 GNSS정보(V2V), 주변 차량의 perception 정보(V2V), 주변 차량의 IMU정보(V2V)
- 교통상황(도로 작업, 교통사고, 스쿨존, 스쿨버스 등 정체요소)에 따른 효율적인 경로 계획 → 교통상황 정보(V2I)
- 노면 정보에 따른 경로 계획 → 노면 상태 정보(V2I)
- 신호등 신호 확인을 통한 효율적인 경로 계획 → 신호등 신호 정보(V2I)
- 전력망 상황 공유를 통한 충전소 경로 계획 → 충전소 사용 현황 정보(V2I)

# Reference

[1] C-ITS 홍보관, [www.c-its.kr](http://www.c-its.kr), 2022.11.11 인용

[2] V2X 기술소개, [http://carnavi.com/v2x](http://carnavi.com/v2x), 2022.11.11 인용

[3] 미국이 선택한 C-V2X 자유주행기술 V2X 알기[https://mytrivia.tistory.com/131?category=822697](https://mytrivia.tistory.com/131?category=822697), 2020.11.22

[4] 호서대학교, 임태호, 자율주행과 V2X 통신 기술 동향, 2022.11.11 인용

[5] 한국과학기술원, 정승재, 강준혁, Millimeter wave 기반 V2I, V2V 통신 기술 연구 동향 및 발전 방향, May, 2017

[6] [기고] 자동차와 모든 것을 연결하는 V2X, 어떻게 5G가 가능하게 하는가, [https://www.elec4.co.kr/article/articleView.asp?idx=29816](https://www.elec4.co.kr/article/articleView.asp?idx=29816), 2022.04.05

[7] [ITS] C-V2X와 DSRC(WAVE)란?, [https://mytrivia.tistory.com/262](https://mytrivia.tistory.com/262), 2022.11.11 인용

[8] [기고] 자율주행 기술: (4) 자율주행차를 가능하게 하는 'V2V/V2I' 통신, [https://www.aitimes.kr/news/articleView.html?idxno=20204](https://www.aitimes.kr/news/articleView.html?idxno=20204), 2021.02.07

[9] NHTSA, “Vehicle-to-Vehicle Communications: Readiness of V2V Technology for Application”, Aug, 2014

[10] 뉴스비전, 5G에 기반한 V2X 통신기술의 진화 ...SKT ·퀄컴, 관련 기술 속속 시연, [http://www.nvp.co.kr/news/articleView.html?idxno=121667](http://www.nvp.co.kr/news/articleView.html?idxno=121667), 2017.11.01

[11] C-V2X와 WAVE, [https://pjy5457.tistory.com/9](https://pjy5457.tistory.com/9), 2018.10.15

[12] 한국전자기술연구원(ETRI), 자율협력주행 지원 V2X 통신 플랫폼 기술, [https://www.youtube.com/watch?v=Aui7_ORl6lE&t=483s](https://www.youtube.com/watch?v=Aui7_ORl6lE&t=483s), 2021.12.24

[13] 자율주행 필수 인프라 C-V2X 기술 알아봅시다, [https://www.youtube.com/watch?v=wFpzAW4mm5M](https://www.youtube.com/watch?v=wFpzAW4mm5M), 2020.12.29

[14] V2X, 안전한 자율주행 완성하다., [https://www.youtube.com/watch?v=fn2fxZNriGE](https://www.youtube.com/watch?v=fn2fxZNriGE), 2020.12.11

[15] Gigabyte, About V2V, [https://www.gigabyte.com/Glossary/v2v](https://www.gigabyte.com/Glossary/v2v), 2022.11.11 인용

[16] 정보통신신문, V2X 자율주행 데이터 개방 속도낸다, [https://www.koit.co.kr/news/articleView.html?idxno=86104](https://www.koit.co.kr/news/articleView.html?idxno=86104), 2021.06.24

[17] TTA, 미래형 교통시스템을 구축하라!,  [https://www.tta.or.kr/data/2019_wellmade/html/sub10.html](https://www.tta.or.kr/data/2019_wellmade/html/sub10.html), 2022.11.11 인용

[18] 서울특별시 빅데이터 제공서비스 신호제어기 신호 정보 서비스, [https://t-data.seoul.go.kr/category/dataviewopenapi.do?data_id=10119](https://t-data.seoul.go.kr/category/dataviewopenapi.do?data_id=10119), 2022.11.11 인용

[19] R.Xu, H.Xiang et al., V2X-ViT: Vehicle-to-Everything Cooperative Perception with Vision Transformer, ECCV, Aug, 2022

[20] 인하대학교, 강민수, 원종훈, EKF와 PF를 활용한 Lidar 및 V2X 기반 협력 위치 추정 기법, 2022.11.11 인용 

[21] TH Wang et al., V2VNet: Vehicle-to-Vehicle Communication for Joint Perception and Prediction, ECCV, Aug, 2020

[22] Yanjun Shi et al., A 5G-V2X Based Collaborative Motion Planning for Autonomous Industrial Vehicles at Road Intersections, IEEE SMC, 2018

[23] 국민대학교, V2X 정보를 활용한 VRU 충돌 회피 알고리즘 개발, 한국ITS학회논문지, Feb, 2022