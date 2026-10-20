# 타이타닉 생존자 예측 (Titanic Survival Prediction)

Kaggle **Titanic** 데이터셋으로 탐색적 데이터 분석(EDA)과 특징 공학을 수행하고, 여러 분류 모델로 승객의 생존 여부를 예측했습니다.

## 데이터셋

- `titanic.zip`: Kaggle Titanic: Machine Learning from Disaster(train/test)
- 주요 변수: `Survived`(타깃), `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `Cabin`, `Embarked`, `Name`

## 소스 구성

```text
Pattern_Titanic_Survival_Prediction/
├── 2주차실습_정회성_2025254014.ipynb  # EDA → 특징 공학 → 모델 비교 → 예측
└── titanic.zip
```

## 분석 내용

1. **EDA**: 생존 비율, 그리고 성별·객실 등급·나이·동승 가족 수·탑승 항구·요금에 따른 생존률을 분석했습니다.
2. **특징 공학**
   - 나이: 결측치(177개)를 중앙값으로 채우고, 10세 단위 연령 그룹(AgeGroup)을 만들었습니다.
   - 객실 번호: 첫 글자만 추출하고, 결측치는 `U`로 처리했습니다.
   - 탑승 항구: 결측치를 최빈값(`S`)으로 채웠습니다.
   - 요금: 결측치를 중앙값으로 채우고, 사분위 구간으로 나눴습니다.
   - 성별: 범주형으로 인코딩했습니다.
   - 이름: 호칭(Title)을 추출했습니다.
   - 가족 규모(FamilySize) 변수를 만들고, 불필요한 변수를 제거했습니다.
3. **모델 비교**: KNN, Decision Tree, SVM, Random Forest를 교차 검증(`cross_validate`)으로 비교했습니다.
4. **특징 선택**: Random Forest의 특징 중요도로 변수를 선택했습니다.
5. **예측**: 테스트 데이터를 예측하고 `submission_result.csv`를 만들었습니다.

## 결과 (교차 검증 정확도)

| 모델 | 학습 정확도 | 검증 정확도 |
| --- | --- | --- |
| KNN | 0.845 | 0.796 |
| Decision Tree | 0.920 | 0.809 |
| SVM | 0.829 | 0.814 |
| SVM (특징 선택 후) | 0.835 | **0.829** |
| Random Forest | 0.903 | 0.814 |

- Kaggle 제출 점수(SVC): **0.77033**

## 실행 방법

```bash
pip install pandas numpy matplotlib seaborn scikit-learn missingno
jupyter notebook "2주차실습_정회성_2025254014.ipynb"
```

`titanic.zip`의 압축을 풀어 노트북과 같은 폴더에 두고 실행하세요.
