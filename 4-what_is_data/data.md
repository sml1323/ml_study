# 데이터 유형 (Types of Data)

* 데이터 유형에 대한 다양한 해석을 알아본다.
* 통계학에서 주로 구분되는 데이터 유형의 범주들을 살펴본다.
* 각 데이터 유형의 예시를 확인한다.

## 데이터 유형에 대한 관점

데이터 유형은 접근하는 관점에 따라 다르게 이해될 수 있다.

### 1. 컴퓨터 과학(Computer Science) 관점

컴퓨터 과학에서는 주로 데이터가 시스템 내에서 어떻게 처리되고 저장되는지에 초점을 맞춘다.

* **주요 고려 사항**:
    * 데이터 저장 형식 (Format of data storage)
* **이것이 미치는 영향 (Implication)**:
    * 수행 가능한 연산 (Operations)
    * 필요한 저장 공간 (Storage space)
* **예시 (Examples)**:
    * 부동 소수점 (Floating point)
    * 문자열 (String)
    * 정수형 (Integer) 등

### 2. 통계학(Statistics) 관점

통계학에서는 데이터의 특성과 측정 수준에 따라 데이터를 분류하며, 이는 분석 방법 선택에 중요하다.

* **주요 고려 사항**:
    * 데이터의 범주 및 척도 (Category/scale of data)
* **이것이 미치는 영향 (Implication)**:
    * 적용 가능한 통계적 분석 절차 (Appropriate statistical procedures)
* **예시 (Examples)**:
    * **수치형 데이터 (Numerical Data)**
        * 구간형 (Interval): 예) 섭씨 온도
        * 비율형 (Ratio): 예) 키, 몸무게
        * 이산형 (Discrete): 예) 인구수
    * **범주형 데이터 (Categorical Data)**
        * 순서형 (Ordinal): 예) 학력 (고졸, 대졸, 대학원졸)
        * 명목형 (Nominal): 예) 혈액형 (A, B, O, AB)
| Category             | Type     | 설명 (Description)                                  | 예시 (Example)                      |
|----------------------|----------|----------------------------------------------------|-------------------------------------|
| Numerical (numbers)  | Interval | 의미 있는 간격을 가진 숫자형 척도                      | 온도 (섭씨)                         |
| Numerical (numbers)  | Ratio    | 구간 척도의 특징과 더불어, 의미 있는 0점(절대 영점)도 가짐 | 키 (cm)                             |
| Numerical (numbers)  | Discrete | 임의의 정밀도 없이 딱 떨어지는 값 (주로 정수)         | 인구수                              |
| Categorical (labels) | Ordinal  | 순서 정렬이 가능한 이산형 데이터                        | 학력 (고졸, 대졸 등)                |
| Categorical (labels) | Nominal  | 순서 정렬이 불가능한 이산형 데이터                        | 영화 장르 (SF, 로맨틱 코미디 등)    |