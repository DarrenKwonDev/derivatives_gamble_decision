## 몇가지 가정들

price : 로그 정규 분포(lognormal) 가정  
returns : 정규 분포(normal) 가정. vol에 비해 noisy 하여 예측이 어려움  
$\sigma$: 변동성. returns의 표준 편차. 평균회귀 + 군집(clustering) + fat tail 특성. 통계적 성질이 더 persistent함.

- 당연히 이런 가정들은 현실과 괴리가 있음. 계산의 편의나 수치의 기준이 필요해서 쓰는 것임.
- $CAGR≈μ− \frac{1}{2} \cdot σ^2$ 이라, 변동성은 연평균 성장률에 직접적인 영향을 미침 (μ = 산술평균 수익률, σ = 변동성)
    - 애초에 '(산술)수익률'만 말하는 것은 반 쪽만 말하는 거고, 변동성도 같이 말해야 함.

## annualized vol

$\sigma_{\text{annual}} = \sigma_{\text{monthly}} \times \sqrt{12}$  
$\sigma_{\text{annual}} = \sigma_{\text{weekly}} \times \sqrt{52}$  
$\sigma_{\text{annual}} = \sigma_{\text{daily}} \times \sqrt{252}$

- 표준편차는 시간에 대해 √T 로 스케일링된다는 가정(Brownian motion 기반)
- 한 달 동안 10% 상승했다고 한다면, 연율화된 변동성은 10% \* √12 정도 된다. 대략 34.64%

## vol quadratic drag

$CAGR≈μ− \frac{1}{2} \cdot σ^2$

여기서 '(산술)수익률'에 변동성이 끼치는 피해는 제곱(quadratic, $σ^2$)에 비례한다.  
즉, 변동성이 2배가 되면 피해는 4배가 된다...! 변동성이 그 만큼 수익을 많이 갉아 먹는 요인이다.

직관적으로는,

- -50% 손실을 복구하기 위해서는 100%의 상승이 필요한 반면
- 50% 수익이 원점으로 되돌아가기 위해서는 -33%의 손실만 필요하다.

레버리지를 과하게 쓰면 변동성이 커져서 수익률이 높아보이지만 장기적인 복리 투자를 가정했을 때 (시장에 계속 재투자 가정) CAGR는 오히려 하락할수 있다.  
다만, 스캘핑, 인트라 데이 전량 청산과 같은 경우라면 CAGR는 큰 의미가 없다. 그냥 레버리지를 써서 트레이드 당 수익을 높이는게 더 낫다.

vol drag는:

median
skewness
distribution

## 로그 수익률과 옵션에서의 거리 개념

- 옵션 모델은 보통 가격의 절대 변화보다 로그수익률/변동성 관점에서 움직임을 본다.
- 옵션판에서 행사가 1칸, 2칸 떨어졌다고 해서 위쪽/아래쪽 위험이 대칭이 아님. 같은 strike 거리 != 같은 위험 거리
- 로그 공간에 있어서 하락은 더 큰 하락을 의미한다.

```
100 → 110 = +10% (산술)
log return = ln(110/100) = +9.53%

100 → 90 = -10% (산술)
log return = ln(90/100) = -10.54%
```

- 옵션을 비교하려면, 같은 델타나 log-moneyness 가진 옵션을 비교하는 것이 일반적이다.
- log-moneyness = ln(K/S)

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

## kelly bet size

$$
f = \frac{edge}{odds} = \frac{bp - q}{b}
$$

- b: payoff ratio  
  p: 이길 확률  
  q: 질 확률 (1-q로 표현하기도)

옵션 매도

- negative skew (작게 수익 자주 내다가 한 번에 크게 잃음)
- high win rate
- Kelly 크게 나옴

옵션 매수

- positive skew (계속 읽다가 한 번에 크게 벎)
- low win rate
- Kelly 작게 나옴

Kelly가 가정하는 수익률의 로그 분포라는 점을 고려하면, 실제로는 fat tail 형태라 더 큰 손실을 야기할 수 있어서 full kelly로 때리기보다는 half, quarter kelly를 사용할 것이 권장됨. ([링크](https://blog.moontower.ai/kelly-math-weirdness/))

## Vol 기반 sizing

권고됨. 다만, 왜도가 강하면 vol만으로는 위험을 설명 못한다
