---
layout  : wiki
title   : 변동성은 과거의 값인가 미래를 예측하는 값인가
summary : 
date    : 2024-03-02 17:56:06 +0900
updated : 2024-03-02 17:56:06 +0900
tag     : 
toc     : true
public  : true
parent  : [[/finance]]
latex   : false
resource: 3C8B137C-8A0A-41B5-A150-7261E7363AD7
---
* TOC
{:toc}

변동성이라는 리스크의 일반적인 개념으로써 말은 변화하는 정도를 표시하는 말이라고 생각할 수 있지만. 금융공학에서는 좀더 엄밀하게 로그 수익률의 표준편차라고 정의한다. 이런 움직임을 제곱한것이 표준편차이다. “표준편차”(standard deviation)라는 말은 통계학에서 사용하는 용어이다. 변동성을 이해하기 위해, 먼저 "표준편차"라는 말부터 알아야 합니다. 

### 표준 편차
표준편차는 사물이나 숫자들이 얼마나 평균값(가장 보통이라고 생각할 수 있는 값)에서 멀리 떨어져 있는지를 측정하는 방법입니다.

5살 아이에게 설명한다면, 우리는 "점프하는 거리"의 예를 들 수 있습니다. 상상해봅시다, 철수와 친구들이 멀리 뛰기를 하고 있습니다. 모두가 점프를 하고, 각자 얼마나 멀리 갔는지를 측정합니다. 만약 모든 친구들이 비슷비슷한 거리만큼 점프를 한다면, 우리는 "점프하는 거리에 변동성이 거의 없다"고 말할 수 있어요. 왜냐하면 모두 비슷한 거리만큼 점프를 했기 때문이죠.

하지만, 만약 한 친구가 정말 멀리 점프를 하고, 다른 친구는 그렇게 멀리 점프하지 못한다면, "점프하는 거리의 변동성이 크다"고 말할 수 있습니다. 이 말은 점프하는 거리가 많이 다르다는 뜻입니다. 즉, 친구들이 점프하는 거리가 얼마나 다양한지를 '변동성'이라고 부릅니다.

금융공학에서의 변동성도 비슷한 원리로 이해할 수 있습니다. 사람들이 주식이나 다른 금융 상품을 사고 팔 때, 그 가격이 얼마나 크게 오르락내리락 하는지를 '변동성'이라고 합니다. 만약 모든 사람들이 주식을 같은 가격에 사고 판다면, 그 주식의 변동성은 낮은 것이고, 만약 어떤 날은 가격이 많이 올랐다가 다른 날은 많이 떨어진다면, 그 주식의 변동성은 높은 것이죠.

이처럼 변동성은 우리가 얼마나 큰 변화를 기대할 수 있는지를 알려주는 중요한 단서가 됩니다. 그리고 이런 변동성을 잘 이해하는 것이 금융에서 중요한 결정을 내릴 때 도움이 됩니다.

### 변동성의 종류
실제 변동성(actual) : 과거 자산 가격 데이터를 바탕으로 측정한 변동성  
내재 변동성(implied) : 옵션 가격을 바탕으로 시장 참가자들이 기대하는 미래 변동성

### 변동성은 과거의 값인가? 미래를 예측하는 값인가?
미래의 주가 변동성은 예측하기 불가능, 지금까지 그 주가가 흘러온 역사를 되돌아보며 흘러왔던 대로 주가의 움직임이 연속될 거라는 가정인것이다. 이처럼, 역사적인 흐름 속에서 산출한 변동성을 역사적 변동성(historical volarility)라고 부른다.
이 방법은 변동성을 산출하는 방법 중 쉽고 직관적이라 가장 널리 쓰이는 방법이지만 미래를 예측하는 수치는 아닌것.

