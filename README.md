# 한국어 문장 관계 분류 경진대회 (5위)
- 목적 : 한국어 문장 쌍 분석 모델 개발
- 일정 : 2022.01.28 - 2022.02.28
- 웹페이지 : [한국어 문장 관계 분류 경진대회](https://dacon.io/competitions/official/235875/overview/description)



## 주요 내용
### 1. Back Translation
- monolingual한 데이터셋을 번역기를 통해 인위적으로 augmentation하는 방법
- Label을 유지한 채로 원본 데이터를 타 언어로 번역한 뒤, 다시 원래의 언어로 재번역하는 과정을 통해 다양성 확보
- 이때 학습된 번역기 구축 작업이 필요하지만 단순 labal 분류 문제를 위해선 새로운 번역 모델을 만드는 것은 비효율적이라 판단해 기존에 구축되어 있는 PAPAGO, Googletrans 번역기 활용

### 2. Model
- KoELECTRA : ELECTRA는 Replaced Token Detection, 즉 generator에서 나온 token을 보고 discriminator에서 "real" token인지 "fake" token인지 판별하는 방법으로 학습. 이 방법은 모든 input token에 대해 학습할 수 있다는 장점을 가지며, BERT 등과 비교했을 때 더 좋은 성능을 보임. KoELECTRA는 34GB의 한국어 text로 학습

- RoBERTa : RoBERTa는 BERT의 파생 모델로, 기존 모델에 추가적인 학습 방법을 제시하여 성능을 향상시킴.

### 3. Soft Ensemble
- 모델 학습 시 모델 weight와 예측 확률을 저장하여 soft ensemble
- 원본 데이터에 KLUE nli dev 데이터를 합친 모델의 5-fold 모델(1) + 해석 데이터로 augmentation한 5-fold 모델(2) + 해석 데이터를 원본 데이터와 바꾸고 KLUE nli dev 추가한 데이터의 모델(3) + 모델(1)과 같은 데이터에 KoELECTRA를 적용한 모델(4)를 부분적으로 앙상블

<img width="688" alt="1" src="https://user-images.githubusercontent.com/97178674/186832584-faf7956b-71a7-4e0d-82f3-f9795f342a04.png">

