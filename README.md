# DACON-Credit-Card
## [DACON] 신용카드 사용자 연체 예측 AI 경진대회


## 📌 **대회 설명**

1. 개요 : 신용카드 사용자 데이터를 보고 사용자의 대금 연체 정도를 예측하는 알고리즘 개발

2. 평가 기준 : Logloss



## 📌 **데이터 설명**

1. gender: 성별
2. car: 차량 소유 여부
3. realty: 부동산 소유 여부
4. child_num: 자녀 수
5. income_total: 연간 소득
6. income_type: 소득 분류 ['Commercial associate', 'Working', 'State servant', 'Pensioner', 'Student']
7. edu_type: 교육 수준 ['Higher education' ,'Secondary / secondary special', 'Incomplete higher', 'Lower secondary', 'Academic degree']
8. family_type: 결혼 여부 ['Married', 'Civil marriage', 'Separated', 'Single / not married', 'Widow']
9. house_type: 생활 방식 ['Municipal apartment', 'House / apartment', 'With parents', 'Co-op apartment', 'Rented apartment', 'Office apartment']
10. DAYS_BIRTH: 출생일 (데이터 수집 당시 0부터 역으로 셈, 즉, -1은 데이터 수집일 하루 전에 태어났음을 의미)
11. DAYS_EMPLOYED: 업무 시작일 (데이터 수집 당시 0부터 역으로 셈, 즉, -1은 데이터 수집일 하루 전부터 일을 시작함을 의미. 양수 값은 고용되지 않은 상태를 의미함)
12. FLAG_MOBIL: 핸드폰 소유 여부
13. work_phone: 업무용 전화 소유 여부
14. phone: 가정용 전화 소유 여부
15. email: 이메일 소유 여부
16. occyp_type: 직업 유형
17. family_size: 가족 규모
18. begin_month: 신용카드 발급 월 (데이터 수집 당시 0부터 역으로 셈, 즉, -1은 데이터 수집일 한 달 전에 신용카드를 발급함을 의미)
19. credit: 사용자의 신용카드 대금 연체를 기준으로 한 신용도 (낮을 수록 높은 신용의 신용카드 사용자를 의미함)



## 📌 점수 기록

1. 레포에 올려놓은 xgboost model + 해당 모델에서 하이퍼 파라미터/교차검증 seed/교차검증 n_splits만 다르게 한 것으로 블렌딩 : Leaderboard Public 0.6807545115 

2. 내 모델 (xgboost) 70% + 팀원 분 모델 30%로 블렌딩 : Leaderboard Public 0.6799667352

　　→ 최종적으로 **Leaderboard Public 0.6799667352 | Private 0.66804 으로 52등 / 714 (Top 8%)**



## 📌 앞으로 보완할 점


**1. 모델 선택**

우승자들 노트북을 보니 catboost가 가장 성능이 좋았다. 나같은 경우에는 대회 초반부에 xgboost를 포함하여 catboost와 lightgbm를 사용해봤지만 처음에는 xgboost 성능이 훨씬 잘 나왔기도 하고 내가 알고리즘에 대한 이해가 부족해서 이 대회는 xgboost가 가장 적합하다고 생각했었다. 예를 들어 그동안 나는 catboost가 범주형 변수가 많을 때 사용하는 것이 좋다고 생각하여 이 대회에서는 범주형 변수의 label 종류가 적은 편이고 데이터의 차원도 크지 않아 catboost보다는 xgboost를 사용하여 하이퍼 파라미터를 최적화해주는 것이 좋겠다고 판단했던 것이다. 
그래서 처음에 이렇게 속단하고 나중에 다른 알고리즘으로 다시 모델링 해볼 생각을 안했다는 점에서 아쉬움이 있다. 다음에 새로운 대회에 참가한다면 하나의 모델로 처음에 속단하지 않고 계속해서 모든 알고리즘으로 모델링을 돌려봐야 겠다고 다짐했다. 또한 다양한 알고리즘에 대한 논문들을 많이 읽고 알고리즘별 특징과 장단점을 제대로 숙지해두어야 겠다고 느꼈다. 


**2. 파생변수**

이것도 크게 보면 모델링과 관련한 아쉬움인데, 사실 파생변수는 다양하게 실험해봤지만 막상 새로운 변수를 추가했을 때 xgboost에서 평가 점수가 떨어지는 경우가 많아서 결국엔 거의 다 제거했다. 그리고 lightgbm에서는 과적합이 많이 되어서 교차검증에선 파생변수를 추가해줄수록 평가 점수가 매우 높게 나왔지만 리더보드에선 떨어졌기 때문에 lightgbm은 사용하지 않았다. 또한 catboost로는 다양한 파생변수를 시도해보지 않았다는 점에서 아쉬움이 있다. 이것도 결국엔 내가 알고리즘에 대한 이해가 부족했다는 문제와 연결되어 앞으로는 관련 논문을 많이 읽어야 겠다는 결론을 내렸다. 


**3. 앙상블 방법**

대회 참여 당시 스태킹을 시도해보지 않았고 블렌딩으로만 앙상블을 했는데 앞으로는 스태킹도 시도해보고자 한다. 


**4. 하이퍼 파라미터 튜닝**

베이지안 최적화로 하이퍼 파라미터 튜닝을 했는데 대회 종료 후 데이콘 코드 공유에서 dswook 님이 공유해주신 optuna 라는 방법을 알게 되었다. 앞으로 optuna으로도 시도해봐야 할 것 같다. 
https://dacon.io/codeshare/2704?dtype=recent



## 📌 느낀 점

전체적으로 아직 공부해야 할 부분이 많구나를 느꼈다. 머신러닝 알고리즘별 특징이나 장단점은 이론적으로 알고 있었지만 막상 실제로 적용해보니 사실상 내가 제대로 이해하지 못한 부분이 있다는 것을 깨달았다. 그래서 책이나 기술 블로그만 참고하지 않고 심층적인 논문들도 많이 읽어야 겠다고 생각했다.

즉, 앞으로 논문 리뷰를 통해 알고리즘을 제대로 이해하고 그것을 실제적으로 적용하면서 이론적으로 내가 이해한 것이 맞는지를 검증해보는 과정이 필요할 것 같다. 
