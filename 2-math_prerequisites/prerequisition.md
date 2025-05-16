
## 1. Math notation - Code (수학 표기법 - 코드)

* `y = e^x`
* `y = ln(x) = log_e(x)` (자연로그)
* `y = log_10(x)` (상용로그)
* `y = exp(x)` (`e^x`와 동일한 표현)
* `y = log(x)` (일반적으로 자연로그 또는 상용로그를 의미)
* `y = log_10(x)` (상용로그)

## 2. 로그와 지수함수는 역함수 (Logarithmic and Exponential functions are inverse functions)

* `e^(ln(x)) = x`
* `ln(e^x) = x`
* `log_a(x) = y` 이면 `a^y = x` 이므로,
* `a^(log_a(x)) = x`

## 3. Sigmoid function (시그모이드 함수)

* **함수식**: `f(x) = 1 / (1 + e^(-px))` (또는 `f(x) = 1 / (1 + e^(-βx))`)
* **특징**: S자 형태의 곡선 ("hill curve"라고도 언급됨)
* **그래프**: x축 (-6 ~ 6), y축 (0 ~ 1) 범위에서 S자 형태로 그려져 있음.

## 4. Logistic function (로지스틱 함수)

* **로짓 변환(log-odds)으로부터 로지스틱 함수 유도 과정**:
    * `ln(p / (1-p)) = β` 
    * 양변에 지수 함수를 취함: `exp(ln(p / (1-p))) = e^β`
    * `p / (1-p) = e^β`
    * `p = e^β * (1-p) = e^β - p*e^β`
    * `p + p*e^β = e^β`
    * `p * (1+e^β) = e^β`
    * **결론**: `p = e^β / (1+e^β) = 1 / (e^(-β) + 1) = 1 / (1 + e^(-β))`
        * (마지막 변환은 분모와 분자를 `e^β`로 나눈 결과입니다.)