# VAR, LSTM 모델을 이용한 트렌드 분석 *[VAR](https://github.com/Yun024/NLP_ICT_Trend/blob/main/5.%20VAR%2CLSTM%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%8A%B8%EB%A0%8C%EB%93%9C%20%EB%B6%84%EC%84%9D/5-1.VAR(Final).py)* , *[LSTM](https://github.com/Yun024/NLP_ICT_Trend/blob/main/5.%20VAR%2CLSTM%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%8A%B8%EB%A0%8C%EB%93%9C%20%EB%B6%84%EC%84%9D/5-2.LSTM(Final).py)*

## 모델 설명



### `VAR`

<p align = "center"><img src = "https://github.com/Yun024/NLP_ICT_Trend/assets/52143231/9144421a-a390-43a1-b14d-5e2938ec62ac.png" width = "500" height = "150" ></p>

- 일변량 AR모델을 다변량 AR모델로 확장한 모델로, 예측 및 내생변수의 변화에 따른 효과 분석 등에 자주 활용되고 있음 
- 예측 시점이 예측하고자 하는 해당 변수의 과거 시점뿐만 아니라, 다른 변수의 과거 시점에도 영향을 받음
- 각각의 변수들 간에 영향을 주는 동적 연립 방정식을 통해 미래 시점의 값을 예측함
- 모형에 사용되는 변수가 많지 않아도 일반적으로 우수한 성능을 보인다는 장점이 있음
- 반면에 적은 수의 변수에게도 성능이 영향을 받기 때문에 변수 선정에 주의를 기울일 필요가 있음

</br>

### `LSTM`

<p align = "center"><img src = "https://github.com/Yun024/NLP_ICT_Trend/assets/52143231/05b9fb88-724a-4a2d-b275-9b25790c9939.png" width = "600" height = "200"></p>

- 기존 예측 딥러닝 모델인 RNN이 예측에 사용할 정보가 멀리 떨어져 있는 경우, 학습능력이 떨어지는 '장기 의존성 문제'를 해결한 모델
- tanh 활성화 함수 게이트에 더해, Forget gate, input gate, output gate를 통해 역전파시 기울기값이 급격하게 사라지거나 증거하는 문제 방지
- 총n개년의 연속된 데이터에서 앞의 n-1개년을 통해 학습에 사용되지 않은 1개년을 예측하고, 예측한 데이터와 실제 타겟 데이터와의 차이를 줄여가는 방식 
- 일반적으로 데이터의 양이 많을수록 정확도가 높아지는 경향이 있음
- 학습에 대한 하이퍼 파라미터 조정에 따라 모델의 성능이 달라지기 때문에 추가적인 연구 필요

## 모델의 구성

- VAR은 앞선 4개년을 독립변수로 하여, 다음년도의 값을 예측하는 방식의 모델을 구성
- LSTM은 예측하고 싶은 년도를 기준으로 3년전까지의 데이터를 독립변수로 구성

## 평가 기준

![image](https://github.com/Yun024/NLP_ICT_Trend/assets/52143231/6f5cc6e1-f46c-400d-886b-594862a6e097)

- MSE, R-Square, KL-Divergence score를 사용하였으며, MSE와 KL-Divergence는 낮을수록, R-square는 높을수록 모델의 정확도가 높다고 볼 수 있음
- 모델과 데이터 별 평가 지표를 비교한 결과 VAR모델이 LSTM모델보다 성능이 우수한 것으로 보임


## 트렌드분석결과
- 토픽 별 분포 시계열 그래프(LSTM)
- 토픽 별 분포 시계열 그래프(VAR)
- 토픽 별 주요단어 TOP5 시계열 그래프(VAR)
- 토픽 별 주요단어 TOP5 시계열 그래프(LSTM) 
  - 한 점으로 예측되는 경우가 많아 본 연구에서는 결과만 도출 후 사용하지 않음  
 

