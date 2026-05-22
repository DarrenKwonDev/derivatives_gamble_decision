## payoff convexity

```
S : 기초자산, K : 행사가라 하자,

call 매수 : max(S - K, 0) - premium
    - call 옵션의 payoff = max(S - K, 0)
put 매수 : max(K - S, 0) - premium
    - put 옵션의 payoff = max(K - S, 0)
```

- 선물은 linear한 손익 그래프 형태를 보이지만 옵션의 payoff는 `convex`함.  
  따라서 작은 변동성에서는 오히려 선물보다 수익이 안날수 있지만 변동성이 크기 움직일수록 더 크게 수익을 얻을 수 있음
- 비선형 payoff라는 말은 다른 말로 하면 `gamma exposure` 가 있다는 뜻임.  
  기초자산의 가격 움직임에 비해 파생 상품인 옵션의 가격은 델타대로만 움직이지 않고, 변동된 델타대로 움직이기 때문(델타의 기울기가 고정되어있지 않음)

## 시간가치

```
가격 = 내재가치(payoff) + 시간가치
∴ 시간가치 = 가격 - 내재가치
```

- 내재가치를 지금 당장 옵션 권리를 실행한다고 가정하고 얻을 수 있는 payoff라고 생각하면 편함

## 옵션의 가치에 의한 delta 변화

| CALL delta    | Strike Price | PUT delta    |
| ------------- | ------------ | ------------ |
| 0.5 ~ 1 (ITM) | 3500         | -0.5~0 (OTM) |
| 0.5 (ATM)     | 4000         | -0.5 (ATM)   |
| 0 ~ 0.5 (OTM) | 4500         | -1~-0.5(ITM) |

- 행사가 근처에서 gamma가 제일 큼. 왜냐면 조금만 더 움직이면 ITM라서

## greeks

```
Delta는 기초자산 가격 변화에 대한 옵션 가격의 1차 민감도입니다.
콜옵션은 양의 delta를 가지고, 풋옵션은 음의 delta를 가집니다. 따라서 delta는 옵션 포지션이 기초자산 방향성에 얼마나 노출되어 있는지를 보여주는 지표로 볼 수 있습니다.

Gamma는 기초자산 가격 변화에 따라 delta가 얼마나 변하는지를 나타내는 2차 민감도입니다.
옵션은 선형 상품이 아니기 때문에 spot이 움직이면 delta도 변합니다. 옵션 매수자는 일반적으로 long gamma 포지션이며, 큰 가격 움직임에서 유리한 convexity를 가집니다.

Vega는 implied volatility 변화에 대한 옵션 가격의 민감도입니다.
옵션 매수자는 일반적으로 long vega 포지션이므로 IV가 상승하면 유리하고, 옵션 매도자는 short vega 포지션이므로 IV 상승에 불리합니다.

Theta는 시간 경과에 따른 옵션 가치의 민감도입니다.
옵션 매수자는 만기까지 남은 시간이 줄어들수록 시간가치가 감소하기 때문에 일반적으로 short theta이고, 옵션 매도자는 시간가치 감소를 수익원으로 삼을 수 있기 때문에 long theta입니다.
```

## greeks에서의 l/s

long gamma = gamma exposure가 양수  
short gamma = gamma exposure가 음수

```
delta exposure = 방향성 리스크를 들고 있음
gamma exposure = 방향성 노출이 변하는 리스크를 들고 있음
vega exposure = IV 변동 리스크를 들고 있음
theta exposure = 시간가치 감소/획득에 노출되어 있음
```

예시

```
콜옵션 매수 → long delta, long gamma, long vega, short theta
콜옵션 매도 → short delta, short gamma, short vega, long theta
현물 매수 → long delta, gamma 거의 없음, vega 없음, theta 없음
```

## IV(Implied Volatility)

- 옵션 가격 이론에 따라 도출되는, 옵션 시장 참여자들의 바라보는 기초 자산의 변동성 (다소 심리적이고 주관적임)
    - 공식에서 도출되었다는 점에서 부터 IV는 이미 옵션 가격에 반영된 것으로 봐야한다
    - 옵션에 투자한다면 실제 변동성(RV)가 IV보다 더 크게 실현될 것으로 베팅하는 것임
