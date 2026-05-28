## 몇가지 가정들

price : 로그 정규 분포(lognormal) 가정  
returns : 정규 분포(normal) 가정  
$\sigma$: 변동성. returns의 표준 편차

당연히 이런 가정들은 현실과 괴리가 있음. 계산의 편의나 수치의 기준이 필요해서 쓰는 것임.

## annualized vol

$\sigma_{\text{annual}} = \sigma_{\text{monthly}} \times \sqrt{12}$  
$\sigma_{\text{annual}} = \sigma_{\text{weekly}} \times \sqrt{52}$  
$\sigma_{\text{annual}} = \sigma_{\text{daily}} \times \sqrt{252}$

- 표준편차는 시간에 대해 √T 로 스케일링된다는 가정(Brownian motion 기반)
- 한 달 동안 10% 상승했다고 한다면, 연율화된 변동성은 10% \* √12 정도 된다. 대략 34.64%

## skew

```
25Δ Call Skew = IV(25-delta call) - IV(ATM)
10Δ Call Skew = IV(10-delta call) - IV(ATM)
```

## RR(risk reversal)

```
RR_25 = IV(25-delta call) - IV(25-delta put)
```

$RR\_{25} > 0$ : 풋에 비해 콜이 비쌈. upside tail 주의하는 사람이 더 많음.  
$RR\_{25} < 0$ : 콜에 비해 풋이 비쌈. downside tail 주의하는 사람이 더 많음.

- RR 부호 convention이 다 다름. 부호 말고 실제 데이터를 한 번은 봐야함.
