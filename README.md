# 고객 이탈 예측 모형과 군집별 맞춤 전략

<br>

## 진행기간
> **2024/05/13~05/22**
<br>


## 사용 데이터
> **신용카드 사용 정보 및 고객 이탈 관련 데이터**
<br>

## 개발 환경
> **Python**
<br>

### 역할(팀장)
> **EDA, Data Prerprocessing, Modeling, 보고서 작성**
<br>

## 분석 주제
> **고객 이탈 예측 모형과 군집별 맞춤 전략**
<br>


## 분석 목표

- `고객 이탈 가능성을 예측`하고, 고객을 특성에 따라 군집화하여 각 `군집별 맞춤형 서비스`를 제공함으로써 최종적으로 고객 이탈 감소
    - 이탈 가능성이 높은 고객군을 식별하고 그 특성을 분석
    - 다양한 기계학습 모델을 통해 이탈 예측 정확도를 극대화
        - 이탈 신호를 조기에 포착하여 기업의 서비스 개선책을 마련하고, 고객 만족도를 향상시키며 추가적인 서비스 구매를 유도
    - 고객 군집화를 통해 동질적인 속성을 가진 군집들을 생성하고, 각 군집의 고유한 특성과 요구를 이해
        - 분석 결과를 바탕으로 군집별 맞춤형 서비스 및 마케팅 전략을 제안
    - 고객의 거래 패턴, 서비스 사용 행태, 그리고 다른 데이터를 종합적으로 분석하여 이탈 가능성을 사전에 예측하고, 적극적인 대응 전략 수립
- **분석 결과를 바탕으로 고객 이탈에 끼치는 영향을 파악하고, 군집별 맞춤형 서비스 및 마케팅 전략을 제안하여 고객 만족도를 향상**
- `고객 이탈을 최소화`하고 기업의 장기적인 경쟁력을 확보시키는 실질적인 방안을 제공

<br>

## 문제 정의 및 KPI 설정

- **문제 정의: 고객 이탈 예측 및 방지 전략 개발**
    - 어떤 고객 특성이 이탈에 영향을 끼치는지 파악하고, 이탈 가능성이 높은 고객군을 식별 후 `이탈 방지`를 위한 `전략 수립`
- **KPI**
    - `Macro-average F1 Score`: 각 클래스에 대한 F1 Score를 단순 평균
    - `MCC`: TP, TN, FP, FN을 모두 고려한 측정 지표
    - `매튜스 상관 계수(Matthews Correlation Coefficient, MCC)`: 이진 분류에서 실제와 예측값 사이의 상관관계를 -1부터 1 사이의 값으로 나타내며, 불균형 데이터셋에서도 성능을 정확하게 측정
    - `G-평균(G-Mean)`: 민감도(재현율)와 특이도를 동시에 고려하여, 각 클래스의 예측 성능을 조화롭게 평가하는 척도
- **고객 이탈 예측**: 고객 이탈 여부를 예측하고 그 영향력을 해석 후 이탈 원인을 식별
- **고객 유지 전략**: 고객 세그먼트에 대한 타겟 마케팅 전략을 수립
<br>


## 분석 요약(담당 부분)

1. EDA
    1. Multivariate EDA
    2. 이탈 여부를 중심으로 Univariate EDA
    3. 파생 변수 생성
2. Modeling
    1. Data Augmentation(SMOTE, ADASYN)
    2. Feature Selection
        1. PCA, Truncated SVD
        2. RFE, Lasso
    3. Cross Validation
    4. HyperParameter Tunning
3. 결과 해석
<br>





## 분석 과정

**`Columns`**

|  |  |  |  |
| --- | --- | --- | --- |
| **CLIENTNUM** | 각 고객의 고유 식별자 | **Months_Inactive_12_mon** | 지난 12개월 동안 고객이 활동하지 않은 개월 수 |
| **Attrition_Flag** | 고객 이탈 여부 | **Contacts_Count_12_mon** | 지난 12개월 동안 고객이 연락한 수 |
| **Customer_Age** | 고객 연령 | **Credit_Limit** | 고객 신용 한도 금액 평균(지난 12개월) |
| **Gender** | 고객 성별 | **Total_Revolving_Bal** | 이월된 미납 총 금액 평균(지난 12개월) |
| **Dependent_count** | 고객 부양가족 수 | **Avg_Open_To_Buy** | 구매 가능 신용 한도 금액 평균(지난 12개월) |
| **Education_Level** | 고객 교육 수준 | **Total_Amt_Chng_Q4_Q1** | 4분기 대비 1분기의 거래 금액 변동 |
| **Marital_Status** | 고객 결혼 상태 | **Total_Trans_Amt** | 총 거래 금액(지난 12개월) |
| **Income_Category** | 고객 소득 범주 | **Total_Trans_Ct** | 총 거래 수(지난 12개월) |
| **Card_Category** | 고객이 보유한 카드 종류 | **Total_Ct_Chng_Q4_Q1** | 4분기 대비 1분기의 거래 수 변동 |
| **Months_on_book** | 고객의 계좌 유지 기간 | **Avg_Utilization_Ratio** | 카드 평균 활용률 |
| **Total_Relationship_Count** | 고객이 신용 카드 제공업체와 맺은 총 관계 수(카드, 계좌 등) |  |  |

- 활용한 데이터는 상기 기술된 것과 같이 신용카드 사용 정보와 그에 따른 고객 이탈 여부의 정보를 제공
- 원본 데이터 셋에서는 총 10127개 행과 21개의 열로 구성
- 연령과 성별 등 고객 정보와 관련된 열과 계좌 유지 기간, 활동하지 않은 개월 수, 거래 금액 등 카드 사용 정보와 관련된 상세한 열들로 구성
- 결측은 존재하지 않지만 skew 된 분포를 가지는 변수가 다수 존재
- 지난 12개월의 기간을 평균 내거나 종합하는 식의 변수로 구성되어 있음을 고려
- 타겟 변수인 Attrition_Flag는 이탈한 고객의 비율이 약 16%로 불균형하여 Sampling 기법을 고려


<br>


### *EDA*

**`Multivariate EDA`**

- `HeatMap, Correlation with 이탈여부`

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/29ca79d9-f786-4d3f-adc1-818e48560aa5" width="90%">
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/1b614742-138a-48bd-9b42-e5f264545596" width="90%">
    </td>
  </tr>
</table>

- **음의 상관관계**: Total_Relationship_Count, Total_Revolving_Bal,Total_Amt_Chng_Q4_Q1, Total_Trans_Amt, Total_Trans_Ct, Total_Ct_Chng_Q4_Q1, Avg_Utilization_Ratio
- **양의 상관관계**: Months_Inactive_12_mon, Contacts_Count_12_mon

<br>


- `이탈 여부와 상관관계가 높았던 변수 활용한 pairplot`

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/a1f06e3a-ed12-4e36-8a74-c4ffdd16cba8" width="90%">
    </td>
  </tr>
</table>

- 해당 변수를 통해 시각화 했을 때 변수의 영향을 받아 이탈 여부가 분리되는 경향을 보이는 것을 확인
- 해당 변수들은 이탈 여부를 예측할 시 중요도가 클 것이라고 판단
- 위의 변수를 제외하고 pairplot을 그렸을 시는 무작위로 분포가 나타나는 것으로 확인(시각화 생략).
<br>


**`이탈 여부 중심으로 Univariate EDA`**

> **수치형 변수: BoxPlot 및 Histogram 으로 이탈 여부에 따른 분포 비교 및 구간 분할 후 해당 구간에서 이탈 여부 비율 확인**

> **범주형 변수: 범주별 이탈 여부 비율을 확인**

<br>

***이탈 여부에 따라 분포가 다르거나, 구간 혹은 범주별로 이탈 비율이 다르다면 해당 변수의 변화에 따라 이탈율에 영향을 줄 것***
<br>
<br>

- **아래는 수치형 변수와 범주형 변수의 시각화 및 간단 해석(각각 하나씩 기재, 나머지는 첨부된 보고서 참고)**
    - 수치형 변수의 경우 더 자세한 해석
    - 범주형 변수의 경우 나머지도 크게 이탈율에 영향을 끼지지 않을 것으로 판단되지만, 적절한 조합을 통해 영향을 줄 수 있으므로 차원축소가 진행 됐음을 참고
<br>

- `Total_Ct_Chng_Q4_Q1`

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/419e4710-e03f-4fcb-936a-6263e1a08be7" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/77204ed7-e30d-4627-93f0-a277e5a5123c" width="95%">
    </td>
  </tr>
</table>

- 좌측은 이탈 고객과 그렇지 않은 고객의 분포를 나타내며, 우측은 이를 구간별로 비율로 나타낸 그래프
- 값이 낮을 수록 고객이 이탈할 확률이 높을 것으로 해석되며, 이탈 여부를 예측하는데 중요한 역할을 할 가능성 높음
<br>

- `Education_Level`

<table width="100%">
  <tr>
    <td align="left" width="50%">
      <img src="https://github.com/user-attachments/assets/16607634-c500-4c15-8acf-4a4dd4bef247" width="95%">
    </td>
    <td align="right" width="50%">
      <img src="https://github.com/user-attachments/assets/1a280bbc-e71f-42b6-9f2f-d37e58e45931" width="95%">
    </td>
  </tr>
</table>

- 범주에 따라 이탈에 영향을 크게 끼치지 않는 것으로 보임
<br>

**`파생 변수`**

- **위와 같은 방식으로 EDA 및 해석이 진행됐음을 참고(보고서에 기재됨)**
<br>

- `거래 당 지불 금액`
    - Avg_Trans_Amt = Total_Trans_Amt/Total_Trans_Ct
    - 적은 수의 고객이지만 거래당 지불 수가 일정 구에서 이탈비율이 높게 분포
    - 높은 값을 가지는 고객의 경우 vip 고객 층으로 볼 수 있어 군집화에서 활용 예정
- `거래 기간 대비 총 거래 횟수`
    - Transaction_Frequency = Total_Trans_Ct/Months_on_book
    - 이탈 여부에 따른 분포 차이가 존재
    - 기간 대비 거래 횟수가 적을 수록 이탈율이 높음
- `소득 대비 총 지불 금액`
    - Spending_Rate = Total_Trans_Amt/Approx_Income
    - 소득 대비 지출을 0.3 이상 하는 고객은 매우 적음
    - 특정 구간에서 이탈 비율이 매우 낮음
    - 적절한 지출을 하는 안정적인 고객층으로 판단
- `활동성 지수: 은행과의 상호작용 정도`
    - Activity_Index = {Total_Relationship_Count/max(Total_Relationship_Count)} + {1 - (Months_Inactive_12_mon/12)} + {Contacts_Count_12_mon/max(Contacts_Count_12_mon)} + {Total_Trans_Ct/max(Total_Trans_Ct)}
    - 은행과의 상호작용이 많을 수록 이탈 비율이 낮아지는 것으로 판단
    - 충성고객과 관련하여 군집화에 활용할 가능성

```python
df['Activity_Index'] = (df['Total_Relationship_Count'] / df['Total_Relationship_Count'].max()  # 총 관계 수를 최대 관계 수로 나눈 비율
                        + (1 - df['Months_Inactive_12_mon'] / 12)  # 최근 12개월 동안 활동한 개월 수의 비율
                        + df['Contacts_Count_12_mon'] / df['Contacts_Count_12_mon'].max()  # 연락 횟수를 최대 연락 가능 횟수로 나눈 비율
                        + df['Total_Trans_Ct'] / df['Total_Trans_Ct'].max()) # 총 거래 횟수를 최대 거래 횟수로 나눈 비율

# 각 변수별로 최대값을 이용해 정규화 후 종합하는 방식
```

- `평균 계좌 유지 기간 대비 활동 지수`
    - Engagement_Ratio = Activity_Index/Months_on_book
    - 이탈 여부에 어느 정도 영향을 끼치는 것으로 보이나 활동성 지수보다는 명확하지 않음
- `평균 지출 당 연체 비율`
    - Avg_Trans_Revolving_Ratio = Total_Revolving_Bal / Total_Trans_Amt
    - 비율이 높다면 연체가 더 많은 것이고 낮을 수록 거래 금액 대부분이 상환됐다는 의미
    - 비율이 0에 가까울 때 많은 이탈이 일어난 것을 확인

- `Correlation with 이탈 여부`

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/d2c376bc-5110-4aac-8c46-f4ea175437f8" width="90%">
    </td>
  </tr>
</table>

- 파생변수와 target과의 상관관계도 어느정도 나타나 예측 모델과 군집 모델 모두에 좋은 영향을 끼칠 것으로 예상
<br>

***파생변수가 원본 변수의 조합으로 이루어져 다중공선성 문제가 있을 것으로 예상됨. Feature Selection을 통해 해결하거나 다중공선성에 강한 모델 활용 필요***
<br>

### *Modeling*

> **Modeling에 앞서 Feature Engineering 및 Feature Selection을 진행 후 학습데이터 선정**

> **타겟변수의 클래스가 불균형하여 이를 처리하기 위한 SMOTE와 ADASYN을 활용하여 Data Augmentation을 진행**

> **최종적으로 사용할 변수를 선정하기 위해 PCA, VIF, RFE, Lasso 와 같은 방법을 고려**

<br>

**`Data Augmentation`**

- 원본 데이터 셋을 그대로 학습하기에 타겟변수의 클래스 불균형이 존재하여 이를 해결하기 위해 `SMOTE, ADASYN`을 활용
- 학습데이터와 검증데이터를 7:3으로 나눈 후 수치형 변수는 표준화를, 범주형 변수는 OneHotEncoding을 진행하여 학습을 진행 후 교차검증을 통해 성능을 측정
- Sampling 기법이 모델 성능에 유효한 결과를 가져오는지 확인하기 위해 `Accuracy, F1 score, F1, Macro, MCC, G-Mean`을 중심으로 SMOTE, ADASYN 그리고 원본데이터를 비교하여 성능을 측정
- 모델은 Logistic Regression, Random Forest, GBM, XGBoost 4가지를 활용. 그 결과는 아래와 같음

| Method | Model | Accuracy | F1 Score | F1 Macro | F1 Weighted | MCC | G-Mean |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SMOTE | Logistic Regression | 0.851860 | 0.644489 | 0.775458 | 0.864633 | 0.582532 | 0.847272 |
| SMOTE | Random Forest | 0.954007 | 0.853259 | 0.912994 | 0.953665 | 0.826335 | 0.904412 |
| SMOTE | Gradient Boosting Machine | 0.955559 | 0.865417 | 0.919400 | 0.956157 | 0.839680 | 0.930546 |
| SMOTE | XGBoost | 0.971642 | 0.910154 | 0.946658 | 0.971514 | 0.893535 | 0.941651 |
| ADASYN | Logistic Regression | 0.827028 | 0.617308 | 0.752778 | 0.845018 | 0.556988 | 0.845059 |
| ADASYN | Random Forest | 0.955982 | 0.859854 | 0.916872 | 0.955695 | 0.833997 | 0.909105 |
| ADASYN | Gradient Boosting Machine | 0.954007 | 0.863032 | 0.917698 | 0.954917 | 0.837012 | 0.934971 |
| ADASYN | XGBoost | 0.971360 | 0.908647 | 0.945832 | 0.971150 | 0.891938 | 0.938425 |
| Original | Logistic Regression | 0.905333 | 0.665370 | 0.805117 | 0.900268 | 0.618566 | 0.754361 |
| Original | Random Forest | 0.954148 | 0.843166 | 0.908157 | 0.952410 | 0.821296 | 0.873985 |
| Original | Gradient Boosting Machine | 0.965717 | 0.887342 | 0.933562 | 0.965033 | 0.868651 | 0.914505 |
| Original | XGBoost | 0.972630 | 0.911498 | 0.947655 | 0.972273 | 0.896015 | 0.935270 |

- `원본 데이터`를 활용한 `XGBoost` 가 전반적으로 성능이 가장 좋게 측정
- 데이터 불균형 처리는 불필요할 것으로 판단
<br>

**`Feature Selection`**

> **상기 기술된 Univariate EDA에서 Total Trans Amt의 경우 다봉 분포를 나타내어 적절한 변수 변환으로 성능을 향상 시킬 수 있다고 판단. Clustering을 통해 군집을 생성하고 해당 군집 번호를 새로운 변수로 할당. 이 때 원본 변수를 사용했을 때와 군집 번호 변수를 사용했을 때의 성능 비교**

> **범주형 변수의 경우 단일 열로는 이탈 여부에 영향을 큰 영향을 끼치지  않을 것으로 확인되나, 조합적으로 보았을 때는 영향이 있을 것으로 판단. 이에 차원 축소를 통해 해당 변수를 예측 모델 변수로 활용. PCA와 Truncated SVD 활용**

> **여러 변수간 상관관계가 높기도 하고, 파생 변수를 생성 시 원본 변수를 조합한 결과이기 때문에 다중공선성 문제가 발생함. 이에 RFE, Lasso 방식을 활용하여 Feature Selection을 진행 하고 해당 결과가 성능 향상에 도움을  주는 지 확인**

<br>

***학습데이터와 검증데이터를 7:3으로 나눈 후 수치형 변수는 표준화를, 범주형 변수는 OneHotEncoding을 진행하여 학습을 진행 후 Accuracy와 F1 score를 기준으로 성능 비교***

***Logistic Regression, Random Forest, XGBoost 모델 사용***
<br>

- `원본 데이터 활용 시 성능(base)`
<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/08576381-b9e4-49fc-aa5a-2eb158d496fb" width="90%">
    </td>
  </tr>
</table>
<br>
<br>

- `Total Trans Amt 범주화 여부`
    - 변수 변환을 진행 했을 시 성능이 더 낮아지는 것을 보아 원본 변수를 그대로 사용하기로 결정
    - Feature Importance의 경우를 살펴볼 때도 원본 변수 그대로 사용했을 때 중요도가 높은 편. 물론 변수 변환 이후 0번 클러스터에 해당하는 변수도 중요도가 높지만 나머지 변수의 경우 중요도가 거의 0에 가깝에 계산되는 것을 확인
- `범주형 변수 차원  축소`
    - 범주형 변수를 OneHotEncoding을 진행 후 차원축소 기법 활용
    - 누적 설명력 90% 이상이 되는 시점까지의 성분을 선택
        - 누적 설명력이 90% 이상이 되는 12개의 주성분을 선택
    - OneHotEncoding을 진행하기 때문에 Sparse Matrix가 형성되어 이러한 경우 Truncated SVD가 더 좋은 결과를 도출할 것으로 기대했으나 결과적으로 PCA가 더 우세
- `RFE, Lasso`
    - 원본 데이터 셋을 그대로 사용하기에도 변수 간 상관관계가 있으며, 파생 변수로 인해 `다중공선성 문제`는 확실히 존재
    - RFE와 Lasso를 활용하여 변수를 줄여 다중공선성 문제를 해결하고자 함(VIF 지표 확인)
    - **RFE, Lasso 모두 가장 최적화된 성능을 가지게 자동으로 규제 강도를 결정하도록 설정한 모델과 직접 다중공선성 문제가 해결되는 부분까지의 규제를 넣어 확인**
        - **다중공선성이 해결될 정도로 변수를 삭제 시 성능이 매우 저하**
    - **결과적으로 Feature Selection으로 인해 성능이 저하되었고 모든 변수를 그대로 사용하는 것이 가장 성능이 좋음**
    - 다중공선성 문제를 해결하지 않는 것이 성능에 도움이 되므로 `다중공선성 문제에 강한 모델을 활용`하기로 판단

<br>

**`최종 데이터 세트`**

> **수치형 변수는 특별한 변환 없이 사용: skew 된 부분은 추후 표준화 혹은 Box-Cox 변환이 진행 됨을 참고**

> **범주형 변수는 OneHotEncoding 후 PCA를 통해 누적 설명력 90% 이상이 되는 12개의 주성분으로 변환**

> **파생 변수 5개 추가**

> **최종적으로 모두 수치형 변수로 볼 수 있으며 총 33개의 열로 구성**
<br>

**`Cross Validation`**

> **모델의 일반화를 위해 Cross Validation 과정 진행**

> **다중 공선성 문제가 남아있으므로 이에 강건한 모델을 선정하여 확인**

> **XGBoost, RandomForest, ExtraTree, SVM, GBM, LGBM, Neural Networks 모델 사용(성능 확인 지표는 Accuracy와 F1 Score)**

```
Random Forest - Accuracy CV scores: [0.95627645 0.95275035 0.95980254 0.95201129 0.96471418]
Random Forest - F1 Score CV scores: [0.84951456 0.84235294 0.86651054 0.8411215  0.88207547]
Extra Trees - Accuracy CV scores: [0.9393512  0.94076164 0.94569817 0.9350741  0.95130558]
Extra Trees - F1 Score CV scores: [0.77720207 0.78571429 0.80407125 0.76767677 0.82878412]
Gradient Boosting - Accuracy CV scores: [0.95980254 0.96473907 0.96544429 0.96471418 0.96400847]
Gradient Boosting - F1 Score CV scores: [0.86396181 0.8853211  0.88683603 0.88372093 0.88056206]
SVM - Accuracy CV scores: [0.93229901 0.93018336 0.94358251 0.92872265 0.93719125]
SVM - F1 Score CV scores: [0.75879397 0.75675676 0.80487805 0.75425791 0.78345499]
XGBoost - Accuracy CV scores: [0.96755994 0.9696756  0.96897038 0.97177135 0.98023994]
XGBoost - F1 Score CV scores: [0.89302326 0.90205011 0.9009009  0.90909091 0.93636364]
LightGBM - Accuracy CV scores: [0.96826516 0.97179126 0.97390691 0.96753705 0.97459421]
LightGBM - F1 Score CV scores: [0.8951049  0.90990991 0.91609977 0.8963964  0.91705069]
Neural Network - Accuracy CV scores: [0.93018336 0.9280677  0.93441467 0.9308398  0.93860268]
Neural Network - F1 Score CV scores: [0.76705882 0.76923077 0.79379157 0.78508772 0.80272109]
```

- 모델 모두 일반화에는 문제 없는 것으로 파악되나 성능에 차이가 존재
- 최종 모델은 Random Forest,  GBM, XGBoost, LightGBM 으로 선정
<br>

**`HyperParameter  Tunning`**

> **최종 선정된  Random Forest,  GBM, XGBoost, LightGBM 모델과 이를 Soft Voting 방식을 사용한 Ensemble 모델로 총 5가지 모델을 활용한다,**

> **수치형 변수의 경우 Skew 된 경향을 띄는게 존재하여 표준화 후 학습하는 방식과 Skewness가 0.5 이상인 경우 Box-Cox 변환 후 표준화하는 방식 2가지 방식으로 나누어 Tunning을 진행했다(Scoring은 F1 macro)**
<br>

- `최종 선택된 HyperParameter`

```
Random Forest: {'model__max_depth': None, 'model__min_samples_split': 2, 'model__n_estimators': 100}
GBM: {'model__learning_rate': 0.3, 'model__max_depth': 5, 'model__n_estimators': 500}
XGBoost: {'model__learning_rate': 0.2, 'model__max_depth': 3, 'model__n_estimators': 300, 'model__subsample': 1}
LGBM: {'model__learning_rate': 0.3, 'model__n_estimators': 300, 'model__num_leaves': 31}
```
<br>

- `최종 모델 성능`

<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/7c460f5e-a840-4a03-997c-298fb047cd88" width="90%">
    </td>
  </tr>
</table>

- Ensemble 모델이 가장 우수한 성능
- 원본 데이터를 활용하여 튜닝하지 않은 모델과 성능을 비교해서 확연한 차이는 보이지는 않으나 전반적으로 모든 모델에서 성능이 증
- 범주형 변수의 PCA와 파생  변수 생성 그리고 Skew된 분포의 Box-Cox 변환은 성능 향상에 유효한 것으로 판단
<br>

- `Ensemble 모델의 Feature Importance`
<table width="100%">
  <tr>
    <td align="center">
      <img src="https://github.com/user-attachments/assets/f7d6baf1-3975-4555-8df9-81dd64dec56c" width="90%">
    </td>
  </tr>
</table>
- 상위 12개 중 생성한 파생 변수가 모두 포함되어 유의미한 파생 변수들임을 확인

<br>
<br>

### *결과 해석*

- **이탈 여부의 클래스가 불균형하지만 따로 처리하지 않을 때가 가장 성능이 우수. 이는 원본 데이터에서 충분히 이탈 여부를 판별할 수 있도록 특성이 설명되며 Sampling을 진행 시 오히려 노이즈가 증대되어 성능이 낮아질 수 있음을 암시**
- **성능 기준으로 `f1_macro score`를 사용하였는데 이는 각 클래스에 대한 F1 점수를 계산하고 그 결과를 평균 내어 클래스 불균형을 고려하지 않고 각 클래스를 동일하게 취급**
    - **이 방법은 클래스 별 샘플 크기가 다를 때 유용. 본 분석에 불균형 처리를 따로 진행하지 않았기 때문에 가장 적절한 성능 지표로 판단**
- **`파생 변수 생성`은 성능에 더 좋은 영향을 끼침을 확인**
- **skewness 가 0.5 이상일 경우 `Box-Cox 변환` 후 표준화를 진행했을 때 가장 성능이 우수**
- **범주형 변수의 경우 OneHotEncoding 후 `PCA`를 진행하여 누적 설명력이 90% 이상이 되는 주성분을 선택하여 진행 시 성능이 가장 우수**
- **다중공선성 문제가 발생하여 RFE, Lasso 등의 방식을 활용해보았으나 결과적으로 모든 변수를 활용했을 때 가장 우수한 성능을 보여 다중공선성에 강건한 모델을 선정**
- **XGBoost, RandomForest, LGBM, GBM 모델과 이를 Soft Ensemble 한 모델을 최종적으로 선정되었으며 튜닝을 진행**
- **`Soft Ensemble 모델`이 가장 우수한 성능을 보임**
<br>

- **`Feature Importance 상위 12개를 중심으로 이탈 원인 해석 및 이탈 방지 전략 수립`**
    - **Total_Trans_Amt 및 Total_Trans_Ct**:
        - 고객의 총 거래 금액이 많을수록 이탈 가능성이 낮아짐을 보여주는 가장 높은 Feature Importance를 지닌다. 적극적인 거래는 고객의 은행 제품에 대한 의존성을 나타내며 만족도가 높다는 신호로 해석될 수 있다.
        - 이탈 방지 전략: 거래를 자주 하고 금액이 큰 고객에게 추가 혜택을 제공하고, 거래 횟수가 많은 고객을 위한 로열티 프로그램을 통해 보상을 제공하여 이들의 활동을 장려할 필요가 있다.
    - **Total_Amt_Chng_Q4_Q1 및 Total_Ct_Chng_Q4_Q1**:
        - 거래 금액과 횟수의 큰 변동은 고객의 금융 활동 변화를 반영하며, 급격한 감소는 불만족이나 서비스 이탈로 이어질 수 있다.  단일열 분석에서도 확연히 값이 높을 수록 이탈 비율이 현저히 낮아짐을 볼 수 있었다.
        - 이탈 방지 전략: 거래 금액이 급감한 고객을 대상으로 조사를 실시하고, 맞춤형 솔루션을 제공하여 문제를 해결하며 만족도를 높일 수 있다. 거래 횟수 감소 고객에게는 새로운 프로모션을 제공하거나, 특별 이벤트를 통해 다시 활성화시키는 전략을 구사할 필요가 있다.
    - **Avg_Trans_Amt**:
        - 평균 거래 금액이 높다는 것은 고객이 더 값비싼 상품이나 서비스를 이용하고 있다는 것을 의미한다. 적은 수의 고객이지만 일정 구간의 값을 가질 때 이탈 비율이 높게 분포한다. 특히 이 변수는 VIP 고객층과 직결되는 변수로 고객 세그먼트 분류에 활용할 수 있다.
        - 이탈 방지 전략: 고가의 거래를 자주하는 고객에게 프리미엄 서비스를 제공하여 이들의 만족도를 극대화할 필요가 있다.
    - **Customer Age**:
        - 단일열 분석에서는 큰 영향이 없을 것으로 보였으나, 다른 변수와 조합하면서 이탈에 영향을 끼친 것으로 판단된다.
        - 이탈 방지 전략: 연령대별 맞춤 서비스를 제공하고, 특정 연령층이 선호할 수 있는 프로모션을 개발하여 고객 만족도를 높일 필요가 있다.
    - **Activity Index**:
        - 활동성 지수가 높은 고객은 은행과의 다양한 상호작용을 자주 하며, 이들의 이탈 가능성이 낮다. 또한 충성 고객군과 직결된 변수로 활용할 수 있다.
        - 이탈 방지 전략: 활동성이 높은 고객에게 추가적인 혜택과 인센티브를 제공하여 활동을 유지하도록 장려할 필요가 있다.
    - **Total Revolving Bal**:
        - 이월된 미납금이 많은 고객은 신용 관리에 어려움을 겪을 수 있으며,  단일열 분석에서도 볼 수 있었듯 매우 높은 값의 미납금을 가지는 고객 층은 이탈 비율이 높다.
        - 이탈 방지 전략: 높은 이월 잔액을 가진 고객을 대상으로 신용 상담 서비스를 제공하여 금융 건강을 돕고 관계를 강화할 필요가 있다.
    - **Transaction Frequency**:
        - 거래 빈도가 높은 고객은 더 자주 은행 서비스를 이용할 가능성이 높으며, 이는 고객 이탈을 예방하는 중요한 요소가 될 수 있다. 단일열 분석에서도 볼 수 있듯 높은 값을 가질 수록 이탈 비율은 현저히 낮아진다.
        - 이탈 방지 전략: 높은 거래 빈도를 지닌 고객에게 더 나은 거래 조건이나 보상을 제공하여 충성도를 증가시킬 필요가 있다.
    - **Engagement Ratio**:
        - 계좌 유지 기간에 비해 높은 활동을 보이는 고객은 은행과 강한 연결고리를 가지고 있으며, 이는 고객 충성도와 직결될 수 있다.
        - 이탈 방지 전략: 고객 참여를 증가시키기 위해 개인화된 상호작용을 늘리고, 고객 맞춤형 서비스를 제공할 필요가 있다.
    - **Credit Limit**:
        - 고객의 신용 한도가 높다는 것은 은행이 그 고객에게 높은 신뢰를 보내고 있음을 의미할 수 있으며, 이에 이탈 여부에는 매우 큰 영향은 없을 수 있으나 해당 변수를 중점으로 고객 세그먼트 분석 등에 활용할 수 있다.
        - 이탈 방지 전략: 높은 신용 한도를 가진 고객에게 추가적인 금융 상품이나 투자 기회를 제공할 필요가 있다.
    - **Spending Rate**:
        - 고객의 재정적 건전성을 보여주며, 소득 대비 지출 비율이 높은 고객은 은행 서비스에 대한 의존도가 높다고 볼 수 있다.
        - 이탈 방지 전략: 이러한 고객의 소비 패턴을 분석하고, 소득 대비 지출이 높은 고객에게 예산 관리 및 재정 계획 서비스를 제공하여 더 나은 고객 경험을 제공할 필요가 있다.
<br>

- **고객 세그먼트 분류를 위한 군집화 제언**
    - 위에서 언급한 변수들은 고객의 행동과 특성을 깊이 이해하는 데 중요한 역할을 하며, 이러한 변수들을 활용하여 고객을 여러 그룹으로 분류하는 군집화 작업을 진행할 수 있다.
    - 군집화는 고객의 소비 패턴, 거래 빈도, 금융 건강 등을 기반으로 하며, 각 군집에 대한 맞춤형 마케팅 전략과 서비스를 제공함으로써 더욱 효과적으로 고객 이탈을 방지하고 만족도를 높일 수 있다. 이 과정에서 각 군집의 특성을 정확히 파악하고, 이를 바탕으로 타겟 마케팅과 리텐션 전략을 개발할 수 있다.
    - 위의 분석을 통해 각 변수들이 고객 이탈에 미치는 영향을 깊이 이해하고, 효과적인 이탈 방지 전략을 수립할 수 있을 것이다. 이러한 전략들은 고객의 충성도를 높이고 장기적인 관계를 유지하는 데 기여할 것이다.
    - ***위의 내용을 기반으로 고객 세그먼트 별 맞춤 전략 제시를 Clustering에서 자세히 진행(보고서에 기재)***

<br>

## 시사점 및 보완할 점

- **KPI 설정**
    - 불균형 데이터 셋으로 성능을 높이기 위해 `Macro-average F1 Score, MCC, G-평균` 등의 다양한 지표를 모두 고려하며 학습
- **범주형 변수 차원 축소**
    - 이탈율에 큰 영향이 없는 것으로 보였지만 범주형 변수들의 적절한 조합을 진행 시 영향이 있는 것으로 판단되어 `PCA, Truncated SVD`를 진행
    - OneHotEncodeing을 진행하기 때문에 Sparse Matrix가 형성되어, Truncated SVD가 더 좋은 성능을 보일거라 판단했으나 PCA를 진행했을 때 가장 성능이 좋았음
- **Feature Selection**
    - `RFE, Lasso` 방식을 사용하여 `다중공선성` 문제를 해결하고자 했으나, 오히려 성능이 저하됨
    - 이에 다중공선성에 강한 모델을 사용
- **Data Augmentation**
    - 불균한 데이터 셋으로 `SMOTE, ADASYN`을 활용했지만 원본 데이터 셋이 가장 성능이 좋았음
        - 샘플링 된 데이터들이 노이즈를 증폭시켰을 가능성
        - 원본 데이터에서 충분히 이탈 여부를 판별할 수 있도록 특성이 설명하고 있음을 암시
- **매우 정교한 EDA를 통해 다양한 가설을 도출하고, 창의적이고 의미 있는 파생변수를 생성하여 분석의 깊이를 더함**
    - 유사한 의미를 가지는 변수들을 정규화하여 각 변수의 영향력을 균등하게 조정한 뒤 통합함.
    - 생성된 파생변수를 효율적으로 재활용하는 방식을 적용하여 분석의 효율성과 일관성을 높임
    - …
- **EDA, 파생 변수 생성, 전처리, Feature Selection 등 머신러닝의 전 과정을 세세하게 논리적인 근거를 찾아가며 진행**











