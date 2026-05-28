## event variance

특정 이벤트로 인하여 IV에 영향을 준다면, 일반 거래일 IV(평상시 IV)와 이벤트로 인한 변동을 구분해볼 수 있다.  
이를 수식화해서 표현하자면 아래와 같다.

$$
\sigma_{\text{term}}^2 T = p \cdot \sigma_{\text{event}}^2 + \sigma_{\text{daily}}^2 (T - 1)
$$

여기서 p는 이벤트 발생확률이다. (이미 발생했다면 1로 설정)

- 이를 잘 활용한 글 (https://blog.moontower.ai/links-between-options-and-event-prediction-markets/)

보통 저 p에 대한 확률(odds)를 기반으로 아래와 같은 것들을 생각해볼 수 있다.

- 저 odds가 정당화될 수 있는지 (polymarket이 맞고 옵션이 잘못되었는지, 옵션이 맞고 polymarket이 맞는지는 조사해봐야)
- 확률이 맞다고 친다면, 얻을 수 있는 수익과 확률이 정해졌으므로 베팅액을 정량화할 수 있음 (ex-half kelly)
