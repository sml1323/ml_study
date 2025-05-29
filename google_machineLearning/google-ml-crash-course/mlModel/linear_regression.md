# 1. 선형회귀


- 변수 간의 관계를 찾는 데 사용되는 통계 기법
- ML 컨텍스트 에서 선형회귀는 특성과 라벨의 관계를 찾는다.

자동차의 무게로 연비를 예측하려고 하고, 다음과 같은 데이터 셋이 있다고 가정

| 파운드 (1,000단위, 지형지물) | 갤런당 마일(라벨) |
| :-----------------------: | :-------------: |
|           3.5           |       18        |
|           3.69          |       15        |
|           3.44          |       18        |
|           3.43          |       16        |
|           4.34          |       15        |
|           4.42          |       14        |
|           2.37          |       24        |



![Linear Regression Graph](../../images/linear_regression.png)


그래프의 실제 점들을 통과하는 선을 그려서 자체 모델을 만들 수 있다.

---
## 선형 회귀식
대수학적으로 이 모델은 $y = mx + b$ 로 정의된다.

* $y$ : 예측하려는 값 → 여기서는 마일 당 갤런
* $m$ : 선의 기울기
* $x$ : 입력값인 파운드
* $b$ : y절편

ML 에서는 다음과 같다.
$y' = b + w_1x_1$

* $y'$ : 예측된 라벨
* $b$ : 모델의 편향. 대수방정식에서 $y$절편과 같으며, $w_0$으로도 표현된다. 모델의 매개변수 이며 학습 중에 계산된다.
* $w_1$ : 특성의 가중치. 대수방정식의 기울기와 같은 개념이다. 모델의 매개변수이며 학습 중에 계산된다.
* $x_1$ : 특성 - 입력이다.

---
## 여러 features가 있는 모델

5가지의 특성을 사용하는 모델
$y' = b + w_1x_1 + w_2x_2 + w_3x_3 + w_4x_4 + w_5x_5$

* $x_1$ : pounds
* $x_2$: 배기량
* $x_3$: 가속
* $x_4$: 실린더 수
* $x_5$: 마력

---
## 선형 회귀: 손실
모델의 예측이 얼마나 잘못되었는지 나타내는 숫자 항목
머신러닝에서 손실은 방향은 중요하지 않고, 값 간의 거리만 측정한다. 즉 부호를 제거하기 위해 절댓값을 취하거나 제곱한다.

### 손실 유형
* **$L_1$ 손실**: 예측값과 실제값 간의 차이의 절대값 합계: $\sum | \text{실제 값} - \text{예측 값} |$
    * **평균 절대 오차(MAE)**: L1손실의 평균
* **$L_2$ 손실**: 예측값과 실제 값 간의 제곱 차이의 합계: $\sum(\text{실제 값} - \text{예측 값})^2$
    * **평균 제곱 오차(MSE)**: L2 손실의 평균

### 손실 선택
* **MSE**: 모델이 이상치에 더 가깝지만 대부분의 데이터 포인터와 멀리 떨어져 있음
* **MAE**: 모델이 이상치에서 더 멀리 떨어져 있지만 데이터 포인터와 가까이 있음

## 경사하강법 (Gradient Descent)

손실이 가장 적은 모델을 생성하기 위해 가중치와 편향을 반복적으로 찾는 수학적 기법
모델은 0에 가까운 무작위 가중치와 편향으로 학습을 시작하고 다음 단계를 반복한다.

1.  현재 가중치와 편향으로 손실계산
2.  손실을 줄이기 위해 가중치와 편향을 이동할 방향 결정
3.  결정한 방향으로 이동
4.  1~3 반복


## 예시

**데이터:**

| 파운드 (1,000단위, 지형지물) | 갤런당 마일 (라벨) |
| :-----------------------: | :-------------: |
|           3.5           |       18        |
|           3.69          |       15        |
|           3.44          |       18        |
|           3.43          |       16        |
|           4.34          |       15        |
|           4.42          |       14        |
|           2.37          |       24        |
*(N=7 데이터 포인트)*

**학습 과정:**

가충치와 편향을 0으로 설정하여 학습 시작
* `weight`, `bias` = 0, 0 → 모델: $y' = 0x_1 + 0$

**1. 손실계산 (MSE):**
Loss = $\frac{(18 - 0)^2 + (15 - 0)^2 + (18 - 0)^2 + (16 - 0)^2 + (15 - 0)^2 + (14 - 0)^2 + (24 - 0)^2}{7} = 303.71$

**2. 방향 결정 (기울기 계산):**
각 가중치와 편향에서 손실 함수의 접선 기울기를 계산
* weight slope ($\frac{\partial L}{\partial w}$) = $-\frac{N}{2}\sum(y_i-(wx_i+b))x_i$
* bias slope ($\frac{\partial L}{\partial b}$) = $-\frac{N}{2}\sum(y_i-(wx_i+b))$

→ 가중치와 편향에 0 대입 후 데이터 입력. **경사 계산** 결과:
    * weight slope: -119.7
    * bias slope : -34.3

**3. 파라미터 이동 (업데이트):**
음의 기울기 방향으로 약간 이동하여 가중치와 편향을 업데이트 한다.

$$\text{새 가중치} = \text{이전 가중치} - (\text{small amount} \times \text{가중치 경사도})$$

$$\text{새 가중치} = 0 - (0.01) \times (-119.7)$$

$$\text{새 가중치} = 1.2$$

**4. 반복:**
더이상 손실이 줄어들지 않는 지점, 수렴할때까지 반복한다.



<details>
<summary>MSE 손실 함수의 가중치(w) 및 편향(b)에 대한 기울기 유도 과정 </summary>

## 1. 모델 및 손실 함수 정의

선형 회귀 모델은 다음과 같이 정의된다:
$$ \hat{y}_i = wx_i + b $$
여기서:
- $\hat{y}_i$: $i$번째 데이터에 대한 모델의 예측값
- $w$: 가중치 (weight)
- $x_i$: $i$번째 데이터의 특성(feature) 값
- $b$: 편향 (bias)

평균 제곱 오차 (MSE, Mean Squared Error) 손실 함수 $L$은 다음과 같다 :
$$ L = \frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2 = \frac{1}{N} \sum_{i=1}^{N} (y_i - (wx_i + b))^2 $$
여기서:
- $N$: 전체 데이터 포인트의 수
- $y_i$: $i$번째 데이터의 실제 값

## 2. 가중치 $w$에 대한 편미분 (기울기) $\frac{\partial L}{\partial w}$

손실 함수 $L$을 가중치 $w$에 대해 편미분하여 $w$에 대한 기울기를 구한다.

$$ \frac{\partial L}{\partial w} = \frac{\partial}{\partial w} \left( \frac{1}{N} \sum_{i=1}^{N} (y_i - (wx_i + b))^2 \right) $$

합계의 미분은 미분의 합계와 같으므로, $\frac{1}{N}$과 $\sum$는 밖으로 나올 수 있다:
$$ \frac{\partial L}{\partial w} = \frac{1}{N} \sum_{i=1}^{N} \frac{\partial}{\partial w} (y_i - (wx_i + b))^2 $$

이제 내부의 $(y_i - (wx_i + b))^2$ 항을 $w$에 대해 미분한다. 연쇄 법칙(Chain Rule)을 사용한다.
$u = y_i - wx_i - b$ 라고 하면, $\frac{\partial}{\partial w} (u^2) = 2u \cdot \frac{\partial u}{\partial w}$ 이다.

먼저 $\frac{\partial u}{\partial w}$를 계산한다:
$$ \frac{\partial u}{\partial w} = \frac{\partial}{\partial w} (y_i - wx_i - b) $$
$y_i$와 $b$는 $w$에 대해 상수이므로 미분하면 0이 된다. $-wx_i$를 $w$로 미분하면 $-x_i$가 된다.
$$ \frac{\partial u}{\partial w} = -x_i $$

이제 이를 원래 식에 대입한다:
$$ \frac{\partial}{\partial w} (y_i - (wx_i + b))^2 = 2(y_i - (wx_i + b))(-x_i) $$

이것을 전체 합계 식에 다시 넣는다:
$$ \frac{\partial L}{\partial w} = \frac{1}{N} \sum_{i=1}^{N} 2(y_i - (wx_i + b))(-x_i) $$

정리하면 다음과 같다:
$$ \frac{\partial L}{\partial w} = -\frac{2}{N} \sum_{i=1}^{N} (y_i - (wx_i + b))x_i $$

## 3. 편향 $b$에 대한 편미분 (기울기) $\frac{\partial L}{\partial b}$

손실 함수 $L$을 편향 $b$에 대해 편미분하여 $b$에 대한 기울기를 구한다.

$$ \frac{\partial L}{\partial b} = \frac{\partial}{\partial b} \left( \frac{1}{N} \sum_{i=1}^{N} (y_i - (wx_i + b))^2 \right) $$
$$ \frac{\partial L}{\partial b} = \frac{1}{N} \sum_{i=1}^{N} \frac{\partial}{\partial b} (y_i - (wx_i + b))^2 $$

연쇄 법칙을 사용한다. $u = y_i - wx_i - b$ 라고 하면, $\frac{\partial}{\partial b} (u^2) = 2u \cdot \frac{\partial u}{\partial b}$ 이다.

먼저 $\frac{\partial u}{\partial b}$를 계산한다 :
$$ \frac{\partial u}{\partial b} = \frac{\partial}{\partial b} (y_i - wx_i - b) $$
$y_i$와 $-wx_i$는 $b$에 대해 상수이므로 미분하면 0이 된다.$-b$를 $b$로 미분하면 $-1$이 된다.
$$ \frac{\partial u}{\partial b} = -1 $$

이제 이를 원래 식에 대입한다.
$$ \frac{\partial}{\partial b} (y_i - (wx_i + b))^2 = 2(y_i - (wx_i + b))(-1) $$

이것을 전체 합계 식에 다시 넣는다:
$$ \frac{\partial L}{\partial b} = \frac{1}{N} \sum_{i=1}^{N} 2(y_i - (wx_i + b))(-1) $$

정리하면 다음과 같다:
$$ \frac{\partial L}{\partial b} = -\frac{2}{N} \sum_{i=1}^{N} (y_i - (wx_i + b)) $$

</details>
