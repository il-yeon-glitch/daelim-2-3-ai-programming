# 대림대학교 2026년 1학기 AI 응용 프로그래밍

## 1주차

- ot 진행

## 2주차

- Git 설치
- Python 설치
- Jupyter Notebook 설치

## 3주차

- 깃허브 업로드
# 대림대학교 2026년 1학기 AI 응용 프로그래밍

## 1주차

- ot 진행

## 2주차

- Git 설치
- Python 설치
- Jupyter Notebook 설치

## 3주차

### 출력
```python
print("안녕하세요")
```

### 변수 & 자료형
```python
name = "Yeon"   # str (문자열)
year = 2026     # int (정수)
print(type(name))  # <class 'str'>
```

### 문자열 연결 & f-string
```python
print("machine" + " " + "learning")
print(f"{name}님, 안녕하세요")
```

### 리스트
```python
scores = [10, 20, 30]
print(scores[0])      # 인덱스 접근
print(len(scores))    # 길이
scores.append(40)     # 요소 추가
```

### 반복문
```python
for score in scores:
    print(score)
```

### 조건문
```python
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
else:
    print("F")
```

### 함수
```python
def add_numbers(a, b):
    return a + b
```

---

## 4주차

### zip() - 두 리스트를 묶어 반복
```python
for name, score in zip(students, scores):
    print(name, score)
```

### 딕셔너리
```python
person = {"name": "kim", "age": 20}  # key-value 쌍
print(person["name"])  # 값 접근
person["age"] = 21     # 값 수정
person["gender"] = "male"  # 추가
del person["gender"]   # 삭제
```

### 딕셔너리 + 반복문
```python
for subject, score in scores.items():
    print(f"{subject}: {score}점")
```

### Pandas DataFrame
```python
import pandas as pd

data = {"a": [1, 2, 3], "b": [4, 5, 6]}
df = pd.DataFrame(data)

df["a"]              # 특정 열
df[["a", "b"]]       # 여러 열
df.iloc[0]           # 특정 행
df.iloc[0, 1]        # 특정 값
df.shape             # (행, 열) 수
df.columns           # 열 이름 목록
df.describe()        # 기본 통계 (평균, 최솟값, 최댓값 등)
df.head(3)           # 상위 N줄
```

### 머신러닝 - 의사결정나무 (DecisionTreeClassifier)
```python
from sklearn.tree import DecisionTreeClassifier

X = df[["study_hours", "attendance"]]  # 입력값
y = df["pass_fail"]                    # 정답

model = DecisionTreeClassifier(random_state=42)
model.fit(X, y)           # 학습
model.predict(new_data)   # 예측
```

---

## 5주차

### 모델 정확도
```python
accuracy = model.score(X, y)  # 0.0 ~ 1.0
print(f"정확도: {accuracy * 100}%")
```

### DataFrame 조건 필터링
```python
df[df["attendance"] >= 70]   # 조건에 맞는 행만 추출
df[df["pass_fail"] == 1]
```

### 리스트 컴프리헨션
```python
passed = [s for s in scores if s >= 60]
```

### 람다(lambda) + 조건 표현식
```python
["O" if a == p else "X" for a, p in zip(y, predictions)]
```

---

## 6주차

### 문자열 메서드
```python
text = "Hello, Python!"
text.upper()          # 대문자 변환
text.lower()          # 소문자 변환
"  hi  ".strip()      # 양쪽 공백 제거
"파이썬".replace("파이썬", "Python")  # 문자열 교체 (체이닝 가능)
"a,b,c".split(",")    # 문자열 분할 -> 리스트
"hello"[0:3]          # 슬라이싱
"좋아요" in review    # 포함 여부 (True/False)
```

### 함수 기본값 파라미터
```python
def greet(name, greeting="환영합니다"):
    print(f"{name}님, {greeting}")

greet("대림대")              # 기본값 사용
greet("대림대", "안녕하세요") # 기본값 덮어쓰기
```

### 함수에서 여러 값 반환 (튜플 언패킹)
```python
def min_max(numbers):
    return min(numbers), max(numbers)

low, high = min_max([10, 50, 30])
```

### Pandas 심화

#### 정렬
```python
df.sort_values("korean")                   # 오름차순
df.sort_values("math", ascending=False)    # 내림차순
```

#### 새 열 추가 & 반올림
```python
df["average"] = (df["a"] + df["b"]) / 2
df["average"] = df["average"].round(1)     # 소수점 1자리 반올림
```

#### apply + lambda (조건부 열 추가)
```python
df["grade"] = df["average"].apply(lambda x: "A" if x >= 80 else "B")
```

#### groupby - 그룹별 통계
```python
df.groupby("grade")["average"].mean()   # 그룹별 평균
df.groupby("dept")["name"].count()      # 그룹별 개수
```

---

## 7주차 - 데이터 시각화 (matplotlib)

### 기본 설정 (한글 깨짐 방지)
```python
import matplotlib.pyplot as plt
import matplotlib
import platform

if platform.system() == "Windows":
    matplotlib.rc("font", family="Malgun Gothic")    # 윈도우: 맑은 고딕
elif platform.system() == "Darwin":
    matplotlib.rc("font", family="AppleGothic")      # 맥: 애플 고딕
else:
    matplotlib.rc("font", family="NanumGothic")      # 리눅스: 나눔 고딕

matplotlib.rc("axes", unicode_minus=False)  # 마이너스 깨짐 방지
```

### 그래프 그리는 기본 순서
```
1. plt.figure(figsize=(가로, 세로))  # 도화지 크기 설정
2. plt.plot() / plt.bar() / plt.scatter()  # 그래프 그리기
3. plt.title() / plt.xlabel() / plt.ylabel()  # 제목, 축 이름
4. plt.grid(True)  # 보조선 추가
5. plt.show()  # 출력
```

### 꺾은선 그래프 (Line Chart)
> 시간에 따른 변화를 보여줄 때 주로 사용
```python
plt.plot(x, y, marker="o", color="tomato", linestyle="-", label="레이블")
# marker: 데이터 위치 표시 점 (o, s, ^ 등)
# linestyle: 선 스타일 (-, --, -., :)
# label: 범례에 표시될 이름
```

### 막대 그래프 (Bar Chart)
> 항목별 값을 비교할 때 사용
```python
plt.bar(x, height, color="steelblue")
plt.ylim(0, 100)       # Y축 범위 지정
plt.grid(axis="y")     # Y축 보조선만 표시

# 막대 위에 값 표시
for i, score in enumerate(avg_scores):
    plt.text(i, score + 1, score, ha="center")
    # x좌표, y좌표(막대높이+여백), 텍스트, 수평정렬(left/center/right)
```

### 산점도 (Scatter Plot)
> 두 수치 데이터 간 상관관계를 점으로 표현, 머신러닝에서 특성 간 관계 파악에 사용
```python
plt.scatter(x, y, color="darkorange", s=80, label="레이블")
# s: 점 크기
plt.legend()  # 범례 표시 (label="" 값이 들어감)
```

---

## 9주차 - 데이터 시각화 심화

### 히스토그램 (Histogram)
> 숫자 데이터가 어느 구간에 많이 모여 있는지 보여주는 그래프
```python
plt.hist(data, bins=10, edgecolor="black")
# bins: 구간(막대) 수
# edgecolor: 막대 테두리 색
```

### 파이 차트 (Pie Chart)
> 전체 중 각 항목이 차지하는 비율을 표현
```python
plt.pie(
    data,
    labels=labels,      # 각 조각 항목 이름
    startangle=90,      # 시작 각도 (90 = 12시 방향)
    autopct="%.1f%%"    # 비율 텍스트 표시 (소수 1자리)
)
```

### 히트맵 (Heatmap)
> 숫자의 크기를 색의 진하기로 표현, 상관계수 확인에 자주 사용
```python
corr = df.corr()  # 컬럼 간 상관계수 계산 (-1 ~ 1, 1에 가까울수록 강한 양의 상관관계)

plt.imshow(corr, cmap="Blues")   # 행렬 데이터를 색으로 시각화
plt.colorbar(label="Correlation")  # 색상 기준 바 표시
plt.xticks(range(len(corr.columns)), corr.columns)  # x축 눈금 설정
plt.yticks(range(len(corr.columns)), corr.columns)  # y축 눈금 설정

# 각 칸에 상관계수 숫자 표시
for row in range(len(corr.columns)):
    for col in range(len(corr.columns)):
        plt.text(col, row, f"{corr.iloc[row, col]:.2f}", ha="center", va="center")

plt.tight_layout()  # 요소 겹침 방지 자동 정렬
```

### 두 데이터 비교 꺾은선 그래프
```python
plt.plot(x, y1, marker="o", label="A")
plt.plot(x, y2, marker="s", label="B")
plt.legend()  # 범례 표시
```

---

## 10주차 - 데이터 전처리 (Data Preprocessing)

> 머신러닝 사용 전 데이터를 깨끗하게 정리하는 모든 작업
> 현실 데이터는 오류, 중복, 결측값이 섞여 있음

### 결측값 확인
```python
df.isna()        # 셀 단위로 NaN 여부를 True/False로 표시
df.isna().sum()  # 컬럼별 결측값 개수 합계
```

### 결측값 처리 ① - 평균값으로 채우기
```python
df['컬럼'] = df['컬럼'].fillna(df['컬럼'].mean())
# mean() 외에도 0, 중앙값(.median()), 직전값 등 사용 가능
```

### 결측값 처리 ② - 결측 행 제거
> 결측 비율이 낮을 때(1~5% 이하), 해당 행이 없어도 분석에 영향 없을 때 사용
```python
df.dropna()  # 결측값이 하나라도 있는 행 전체 삭제
```

### 중복 데이터 제거
> 같은 행이 두 번 이상이면 평균/합계/비율 집계가 왜곡됨
```python
df.duplicated()       # 중복 행 여부 True/False로 표시
df.drop_duplicates()  # 중복 행 제거 (첫 번째 행만 남김)
```

### 문자열 공백 제거
> `"Kim" == " Kim"` → False, 공백이 있으면 다른 값으로 인식됨
```python
df['name'] = df['name'].str.strip()   # 앞뒤 공백 제거
df['name'] = df['name'].str.lstrip()  # 앞 공백만 제거
df['name'] = df['name'].str.rstrip()  # 뒤 공백만 제거
```

### 이상치 확인
```python
df.describe()          # 기술 통계 (min, max, 평균 등으로 이상치 의심)
plt.boxplot(df['컬럼'])  # 박스플롯으로 이상치 시각화
```

### IQR로 이상치 제거
> IQR(Interquartile Range): 데이터를 정렬했을 때 가운데 50% 범위
```
1. Q1 = 하위 25% 값
2. Q3 = 상위 25% 값 (= 하위 75%)
3. IQR = Q3 - Q1
4. 정상 범위 = [Q1 - 1.5×IQR, Q3 + 1.5×IQR]
5. 범위를 벗어나면 이상치로 간주
※ 1.5: 일반 기준 / 3.0: 보수적 기준(극단값만 제거)
```
```python
q1 = df['컬럼'].quantile(0.25)
q3 = df['컬럼'].quantile(0.75)
iqr = q3 - q1
lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

df = df[(df['컬럼'] >= lower) & (df['컬럼'] <= upper)]
```

### 전처리 후 새 열 추가 (apply + lambda)
```python
df['pass_fail'] = df['score'].apply(lambda x: 1 if x >= 75 else 0)
df['total'] = df.apply(lambda row: row['price'] * row['quantity'], axis=1)
# axis=1: 행 단위로 적용
```

### 전처리 순서 (권장)
```
1. 원본 복사 (df.copy())
2. 결측값 처리 (fillna / dropna)
3. 중복 제거 (drop_duplicates)
4. 문자열 공백 제거 (str.strip)
5. 이상치 제거 (IQR)
6. 새 열 추가 (apply + lambda)
```

---

## 11주차 - 회귀 모델 입문 (단순 선형 회귀)

### 머신러닝 문제 유형
| 구분 | 예측 결과 | 예시 |
|---|---|---|
| 분류(classification) | 범주, 클래스 | 합격/불합격, 스팸/정상 |
| 회귀(regression) | 연속적인 숫자 | 시험 점수, 매출액, 배송시간 |

### 단순 선형 회귀
> 입력 변수가 **하나**일 때 사용, 직선 관계를 학습
```
예측 점수 = 기울기 × 공부시간 + 절편
```
```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split

X = df[['study_hours']]  # 입력 (2D DataFrame 형태로)
y = df['score']          # 정답

# 훈련/테스트 분리 (7:3)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)

model = LinearRegression()
model.fit(X_train, y_train)   # 학습

print(model.coef_[0])    # 기울기
print(model.intercept_)  # 절편
```

### 회귀 모델 평가 지표
```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score

pred = model.predict(X_test)

mae  = mean_absolute_error(y_test, pred)   # 오차 절대값 평균 (평균 몇 점 틀리는가)
mse  = mean_squared_error(y_test, pred)    # 오차 제곱 평균 (큰 오차에 강한 벌점)
rmse = mse ** 0.5                          # RMSE: 원래 단위로 해석 가능
r2   = r2_score(y_test, pred)              # 설명력 (1에 가까울수록 좋음)
```

### 새 데이터 예측 시 주의사항
```python
# 학습 때 쓴 컬럼명과 동일하게 맞춰야 함
new_data = pd.DataFrame({'study_hours': [7.5]})
predicted = model.predict(new_data)[0]
```

### 회귀선 시각화
```python
x_line = pd.DataFrame({
    'study_hours': [df['study_hours'].min(), df['study_hours'].max()]
})
y_line = model.predict(x_line)

plt.scatter(df['study_hours'], df['score'], label='Actual Data')
plt.plot(x_line['study_hours'], y_line, color='red', label='Regression Line')
plt.legend()
plt.show()
```

---

## 12주차 - 다중 회귀 (Multiple Regression)

> 입력 변수가 **여러 개**일 때 사용
> 단순 회귀보다 더 다양한 정보를 반영해 예측 정확도가 높아짐

### 단순 회귀 vs 다중 회귀
| 구분 | 입력 변수 | 예시 |
|---|---|---|
| 단순 회귀 | 1개 | 공부시간 → 점수 |
| 다중 회귀 | 여러 개 | 공부시간 + 출석률 + 과제점수 → 점수 |

### 다중 회귀 모델 학습
```python
X_multi = df[['study_hours', 'attendance', 'assignment']]  # 입력 변수 여러 개
y_multi = df['score']

X_train_m, X_test_m, y_train_m, y_test_m = train_test_split(
    X_multi, y_multi, test_size=0.3, random_state=42
)

multi_model = LinearRegression()
multi_model.fit(X_train_m, y_train_m)
```

### 계수(Coefficient) 확인
> 계수: 다른 조건이 같을 때, 해당 변수가 +1 되면 예측값이 얼마나 변하는지
```python
coef_df = pd.DataFrame({
    'feature': X_multi.columns,
    'coefficient': multi_model.coef_
})
print('절편:', multi_model.intercept_)
# coef_df 출력 예시:
#      feature  coefficient
#  study_hours     0.84
#   attendance     0.30
#   assignment     0.52
```

### 단순 vs 다중 성능 비교
```python
multi_pred = multi_model.predict(X_test_m)

compare_df = pd.DataFrame({
    'model': ['단순 회귀(공부시간만)', '다중 회귀(3가지 변수)'],
    'MAE'  : [simple_mae, multi_mae],
    'R2'   : [simple_r2, multi_r2]
})
# 결과 예시: 다중 회귀의 MAE가 훨씬 낮고, R2가 1에 가까움
```