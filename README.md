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
