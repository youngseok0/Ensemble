# Ensemble
이 레포지터리에서 설명하는 내용은 파이썬 머신러닝 완벽 가이드 책에 나오는 내용을 정리한 것임<br>
개인적으로 파이썬 머신러닝 완벽가이드를 사서 읽어보는 것을 추천함
### Ensemble이란?
앙상블 학습을 통한 분류는 여러 개의 분류기를 생성하고 그 예측을 결합함으로써 보다 정확한 최종 예측을 도출하는 기법을 말한다.
### 앙상블의 유형
앙상블의 유형에는 보팅(Voting), 배깅(Bagging), 부스팅(Boosting), 스태킹(Stacking)을 포함한 다양한 앙상블 방법이 있다.
### 보팅(Voting)
<img src="https://cdn.discordapp.com/attachments/701041011174015006/701123105283768390/unknown.png" title="Voting" alt="Voting" width="50%"></img><br>
위의 그림은 보팅을 도식화 한 것이다. 보팅은 일반적으로 위의 그림에서 예시를 든 Linear Regression, K Nearest Neighbor, Support Vector Machine과 같은 서로 다른 알고리즘이 같은 데이터 세트에 대해 학습하고 예측한 결과를 가지고 보팅을 통해 최종 예측 결과를 선정하는 방법이다.
### 배깅(Bagging)
<img src="https://cdn.discordapp.com/attachments/701041011174015006/701127163759558696/unknown.png" title="Bagging" alt="Bagging" width="50%"></img><br>
위의 그림은 배깅을 도식화 한 것이다. 배깅은 부트스트래핑 분할 방식으로 샘플링된 데이터 세트를 여러개의 단일 ML 알고리즘(결정 트리 등)으로 개별 예측한 결과를 보팅을 통해서 최종 예측 결과를 선정하는 방법이다. 여기서 부트스트래핑(Bootstrapping) 분할 방식이란 개별 분류기에게 원본 학습 데이터에서 데이터를 샘플링해서 추출하는 방식을 말한다. 데이터를 샘플링할 때에는 데이터가 중첩되는 것을 허용하기 때문에 10000개의 데이터를 10개의 분류기가 나누더라도 각 1000개의 데이터 내에 중복된 데이터가 있을 수 있다. 대표적인 알고리즘으로 랜덤 포레스트가 있다.
### 보팅 유형
위에 설명한 보팅과 배깅은 보팅을 통해 최종 예측 결과를 선정한다고 했다. 이 보팅 방법에는 두 가지가 있는데 바로 하드 보팅과 소프트 보팅이다.
#### 하드 보팅(Hard Voting)
<img src="https://cdn.discordapp.com/attachments/701041011174015006/701247146292412436/unknown.png" title="Hard Voting" alt="Hard Voting" width="50%"></img><br>
하드 보팅을 이용한 분류는 다수결 원칙과 비슷하다. 예측한 결괏값들 중 다수의 분류기가 결정한 예측값을 최종 보팅 결괏값으로 선정하는 것이다. 위의 그림을 예로 들면 분류기들이 레이블을 1로 예측한게 총 3개, 2로 예측한게 총 1개이고, 따라서 레이블 값 1을 최종으로 보팅한다.
#### 소프트 보팅(Soft Voting)
<img src="https://cdn.discordapp.com/attachments/701041011174015006/701248556664750180/unknown.png" title="Soft Voting" alt="Soft Voting" width="50%"></img><br>
소프트 보팅은 분류기들의 레이블 값 결정 확률을 모두 더하고 이를 평균해서 이들 중 확률이 가장 높은 레이블 값을 최종 보팅 결괏값으로 선정한다. 위의 그림을 예로 들자면 레이블이 1일 확률은 (0.7 + 0.2 + 0.8 + 0.9) / 4 = 0.65가 되고 레이블이 2일 확률은 (0.3 + 0.8 + 0.2 + 0.1) / 4 = 0.35가 된다. 따라서 레이블이 1일 확률이 더 높기 때문에 레이블 값 1을 최종으로 보팅한다. 일반적으로 하드 보팅보다 소프트 보팅이 예측 성능이 좋아서 더 많이 사용한다.
### 부스팅(Boosting)
<img src="https://cdn.discordapp.com/attachments/701041011174015006/701138056308326441/unknown.png" title="AdaBoosting" alt="AdaBoosting"></img><br>
위의 그림은 부스팅 알고리즘 중 하나인 AdaBoost를 학습하는 과정을 도식화 한 것이다. 위의 그림을 볼 때, 동그라미가 처진 것은 잘못 분류된 것이고 기호의 크기는 가중치와 비례해서 보면 된다. 부스팅은 여러 개의 분류기가 순차적으로 학습을 수행하되, 앞에서 학습한 분류기가 예측이 틀린 데이터에 대해서는 올바르게 예측할 수 있도록 다음 분류기에게 는 가중치(weight)를 부여하면서 학습과 예측을 진행하는 것이다. 예측 성능이 뛰어나 앙상블 학습을 주도하고 있으며 대표적인 부스팅 알고리즘으로 그래디언트 부스트, XGBoost, LightGBM이 있다.
### 스태킹(Stacking)
<img src="https://cdn.discordapp.com/attachments/701041011174015006/701252540305637457/unknown.png" title="Stacking" alt="Stacking" width="50%"></img><br>
위의 그림은 스태킹을 도식화 한 것이다. 스태킹은 개별 알고리즘으로 예측을 하고, 그 예측한 데이터를 최종적인 메타 데이터 세트로 만들어 별도의 ML 알고리즘으로 최종 학습을 수행하고 테스트 데이터를 기반으로 다시 최종 예측을 수행하는 방법이다. 스태킹은 개별적인 여러 알고리즘을 서로 결합해 예측 결과를 도출한다는 점에서 배깅 및 부스팅과 공통점을 갖고 있다. 하지만 개별 알고리즘으로 예측한 데이터를 기반으로 다시 예측을 수행한다는 차이점을 갖고 있다.<br>
&nbsp;스태킹은 두 종류의 모델을 필요로 한다. 첫 번째는 개별적인 기반 모델이고, 두 번째는 이 개별 기반 모델의 예측 데이터를 학습 데이터로 만들어 학습하는 최종 메타 모델이다. 여기서 메타 모델이라 함은 개별 모델의 예측된 데이터 세트를 다시 기반으로 하여 학습하고 예측하는 방식을 사용하는 모델을 말한다. 스태킹 모델의 핵심은 여러 개별 모델의 예측 데이터를 각각 스태킹 형태로 결합해 최종 메타 모델의 학습용 피처 데이터 세트와 테스트용 피처 데이터 세트를 만드는 것이다.<br>
&nbsp;스태킹을 형실 모델에 적용하는 경우는 그렇게 많지 않지만, 캐글과 같은 대회에서 조금이라도 성능 수치를 높여야 할 경우 자주 사용된다. 스태킹을 적용할 때에는 개별 모델의 개수는 2~3개로는 예측 성능 향상이 힘들어 모델의 개수가 많이 필요하다고 한다. 또 스태킹을 적용한다고 해서 반드시 성능이 향상된다는 보장도 없다. 일반적으로 성능이 비슷한 모델을 결합해 좀 더 나은 성능 향상을 도출하기 위해 적용된다.<br>
&nbsp;스태킹의 과적합을 개선하기 위해 CV 세트 기반의 스태킹 모델을 사용하는데 **나중에 꼭 채워 넣겠다.**
