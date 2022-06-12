# SOLOv6 Project Overview
# Contents
- [Overview](#Overview)
  - [Team](#Team)
  - [Model Define](#Model-Define)
  - [Goal](#Goal)

- [Project](#Project)
  - [Project Structure](#Project-Structure)
  - [모델 정의](#모델-정의)
  - [Web](#Web)

- [Stack](#Stack)
- [Repositories](#Repositories)
- [데모](#DEMO)

# Overview
- Socar의 기업 과제 중 차량 파손 탐지 및 분류 시스템을 주제를 선정해 진행하였습니다.
- AI가 파손 탐지 모델을 사용해 기존의 단순노동을 AI 모델이 처리함으로써 불필요한 작업 제거
- U-net with EfficientNet B4를 기반으로 Custom Loss Function과 Grad-CAM을 통한 Data Imbalance 문제와 부족한 위치 정보를 보완
- Admin UI 구현을 통한 업무 효율성 증대 : Confidence score을 기준으로 모호한 예측 결과 구분, 검수자들의 편의성 고려


## Team
| Name  | Role  | Email                | Position             |
|-------|-------|----------------------|----------------------|
| 강동연   | 팀장    | anfqlc1127@gmail.com | ML engineer,  MLOps  |
| 노지민   | 팀원    | shwlals96@gmail.com  | ML engineer,  MLOps  |
| 이호준   | 팀원    | hoo8799@gmail.com    | Web engineer,  MLOps |
| 이태현   | 팀원    | lts2769@naver.com    | Web engineer,  MLOps |
| 류예나   | 팀원    | yena0773@naver.com   | Project Manager      |

## Model Define
1. Gooing Deeper에서 진행한 쏘카 이용전 사진을 부위별로 분류하는 작업의 고도화
2. 사고 부위를 판별하여 사고 정도에 따라서 분류하는 작업 (scratch, dent, spacing)
3. Accida 기술 블로그 참고 [링크](https://tech.socarcorp.kr/data/2020/02/13/car-damage-segmentation-model.html)

## Goal
1. AI가 파손 탐지 모델을 사용해 기존의 단순노동을 AI 모델이 처리함으로써 불필요한 작업 제거
2. U-net with EfficientNet B4를 기반으로 Custom Loss Function과 Grad-CAM을 통해 Data Imbalance 문제와 부족한 위치 정보를 보완함
3. Admin UI를 구현해 검수자들의 편의성 고려 및 Confidence Score를 기준으로 모호한 예측 결과 구분으로 효율성 증대


# Project
## Project Structure
![project-design](/images/project-design.png)


## 모델 정의
### Base line
- U-net vs U-net with EfficientNet b0 vs Deeplab v3를 비교했을 때 U-net with EfficientNet이 가장 효율적이므로 Base Model로 사용함
![base-line](/images/baseline.png)

### Model
- Teacher model과 student model을 분리하여 기존 mask가 존재하지 않는 image에 대해서도 student model이 더 나은 학습을 할 수있게 하였습니다. 
- 학습시에 Grad-Cam을 사용하여 모델의 성능을 높였고 추론시에는 student model만을 사용하여 추론시간을 감소시켰습니다.  

![teacher-model](/images/teacher-model.png)  
![student-model](/images/student-model.png)  

### Result
- inference result: 최종 model 합성 image
- pseudo mask: teacher model이 생성한 mask

![result](/images/result.png)
![result2](/images/result2.png)

### Serving
- model serving architecture

![torchserve](/images/torchserve.png)

## Web
### Web Structure
![web-structure](/images/web-structure.png)

### Service Usecase
![service-usecase](/images/service-usecase.jpg)
### DB
![data-base](/images/data-base.jpg)

# Stack
- model
  - GCP(Google Cloud Platform)
  - Pytorch
  - OpenCV
  - Wandb
- web
  - Docker
  - MySQL
  - Flask API
- serve
  - GCF(Google Cloud Function)
  - Docker 
  - Torchserve
  - Prometheus
- etc
  - Github
  - Notion 
  - Figma

# Repositories
| Name                                                           | description      |
|----------------------------------------------------------------|------------------|
| [modeling](https://github.com/SOLOv6/modeling)                 | 모델 관련            |
| [model-serving](https://github.com/SOLOv6/model-serving)       | 모델 serve 관련      |
| [Flask-User](https://github.com/SOLOv6/Flask-User)             | Flask-User       |
| [Flask-admin](https://github.com/SOLOv6/Flask-admin)           | Flask-admin      |
| [GCF-http-trigger](https://github.com/SOLOv6/GCF-http-trigger) | gcs-trigger      |

# Demo
![demo](/images/demo.gif)

