# 한국어 문장 관계 분류 경진대회 (5위)
- 목적 : 한국어 문장 쌍 분석 모델 개발
- 일정 : 2022.01.28 - 2022.02.28
- 웹페이지 : [한국어 문장 관계 분류 경진대회](https://dacon.io/competitions/official/235875/overview/description)

# 주요 내용
## 1. Back Translation
- monolingual한 데이터셋을 번역기를 통해 인위적으로 augmentation하는 방법
- Label을 유지한 채로 원본 데이터를 타 언어로 번역한 뒤, 다시 원래의 언어로 재번역하는 과정을 통해 다양성 확보
- 이때 학습된 번역기 구축 작업이 필요하지만 단순 labal 분류 문제를 위해선 새로운 번역 모델을 만드는 것은 비효율적이라 판단해 기존에 구축되어 있는 PAPAGO, Googletrans 번역기 활용

## 2. 모델 soft ensemble
- KoELECTRA, RoBERTa
