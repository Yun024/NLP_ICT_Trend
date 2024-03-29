# LDA모델을 이용한 토픽 분류


<p align = "center"> <img src = "https://github.com/Yun024/NLP_ICT_Trend/assets/52143231/eb8c6de8-859b-48de-ab12-27565da15035.png" width = "700" height = "300"/></p>



- LDA는 토픽모델링 기법 중 하나로, 주어진 문서에 대해 어떤 주제가 있는지 자동으로 찾아내는 알고리즘(일종의 비지도 분류모델)
- 하나의 문서 내에 여러개의 주제가 서로 다른 가중치로 혼합되는 것을 허용하여, 훈련데이터에 대해 과적합 문제를 잘 겪지 않는다는 장점을 가짐
- 일련의 과정을 반복함으로써 단어와 문서를 통한 가장높은 확률을 가진 토픽에 분류
  + 연구자의 판단하에 토픽 개수 K 임의지정
  + 모든 단어를 K개의 토픽 중 랜덤으로 하나의 토픽에 할당
  + 어떤 문서의 단어 w만 잘못된 토픽에 할당되어 있고, w를 제외한 다른 단어들은 전부 올바르게 할당되어 있다고 가정
  + 문서 내 토픽 분포계산 후 토픽 내 단어 분포 계산 

## LDA 모델 학습 및 구축 *[바로가기](https://github.com/Yun024/NLP_ICT_Trend/blob/main/3.%20LDA%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%86%A0%ED%94%BD%20%EB%B6%84%EB%A5%98/3-1.LDA_Optimization_Y_2000.py)*

- LDA 모델 구성
  + min_cf : 모델에 학습된 전체 문헌 내에서 단어의 출현 빈도가 지저한 숫자이하인 단어를 제외하는 옵션(1001로 지정)
  + rm_top : 너무 흔한 단어가 토픽 모델 상위 결과에 등장하는 것을 방지하기 위해 지정한 숫자까지의 최상위 빈도 단어를 제외하는 옵션 
    + (ex: 의, 을 , 를 정책, 연구/ 64로 지정)
  + alpha : 문헌-토픽 디리클레 분포의 하이퍼 파라미터 (0.1로 지정)
  + eta : 토픽-단어 디리클레 분포의 하이퍼 파라미터 (0.01로 지정)
  + tw : 용어 가중치 기법을 정하는 옵션
  + 점별 상호정보량(PMI)를 가중치로 사용하기 위해 tp.TermWeight.PMI로 지정


</br>

<p align = "center"><img src = "https://github.com/Yun024/NLP_ICT_Trend/assets/52143231/767ff7b3-ca37-4e01-bc70-6b69bd45ad2d.png" width ="700" height = "200"/> 

- 일반적으로 coherence score(좌)는 높을수록 perplexity score(우)는 낮을 수록 모델이 데이터를 잘 해석했다고 봄.
  + 이때 perplexity score가 너무 낮다면 해석 상의 어려움이 나타날 수 있음 
- 토픽개수를 5~150개 범위를 5단위로 설정하여 결과 도출 
- 토픽 20개를 기점으로 coherenec score의 변화가 계속 감소하고 있음



</br>

<p align = "center"><img src = "https://github.com/Yun024/NLP_ICT_Trend/assets/52143231/fc814019-38e4-4ab3-a553-ba6818628e4d.png" width ="600" height = "200"/> 

- 20개를 기준으로 토픽 1개 단위의 증감그래프를 그려 15~24개의 범위에서 coherence score의 값이 가장 큰 20개로 최종 토픽 개수 결정 

## LDA모델을 이용한 토픽 분류 분석 *[NTIS](https://github.com/Yun024/NLP_ICT_Trend/blob/main/3.%20LDA%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%86%A0%ED%94%BD%20%EB%B6%84%EB%A5%98/3-2.LDA_Y_2000.py)*, *[Non-NTIS](https://github.com/Yun024/NLP_ICT_Trend/blob/main/3.%20LDA%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%86%A0%ED%94%BD%20%EB%B6%84%EB%A5%98/3-4.LDA(Non-NTIS%20DATA).py)*

- 각 년도와 토픽 별 가장 빈도가 높은 단어 5개씩 나타낸 표
- 연구자의 주관적인 토픽 별 주제 네이밍
- 토픽 간 관계 시각화
- 토픽 별 대표문서 파악
- 토픽 분포 그래프
- 시간에 따른 토픽 별 분포 꺾은선 그래프
- 토픽 별 텍스트 네트워크 *[바로가기](https://github.com/Yun024/NLP_ICT_Trend/blob/main/3.%20LDA%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%86%A0%ED%94%BD%20%EB%B6%84%EB%A5%98/3-3.LDA_Network_2000.py)*



## LDA토픽 모델링 중분류
- 분류 분석을 통해 파악한 ICT 관련 토픽에 대한 LDA 모델 학습 및 구축 재진행 이후 coherence score 및 perplexity score확인 *[바로가기](https://github.com/Yun024/NLP_ICT_Trend/blob/main/3.%20LDA%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%86%A0%ED%94%BD%20%EB%B6%84%EB%A5%98/6-1.Middle_LDA_Optimization.py)*
- 처음으로 실행한 대분류 LDA모델의 모든 토픽에 대한 중분류 LDA모델 학습 및 구축, 분류 분석 등을 자동 실행하여 결과 도출 *[바로가기](https://github.com/Yun024/NLP_ICT_Trend/blob/main/3.%20LDA%EB%AA%A8%EB%8D%B8%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%ED%86%A0%ED%94%BD%20%EB%B6%84%EB%A5%98/6-2.LDA_auto_middle.py)*

