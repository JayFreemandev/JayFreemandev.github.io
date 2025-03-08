---
layout  : wiki
title   : 고성능 블록체인 아키텍처
summary : 
date    : 2025-02-22 03:12:07 +0900
updated : 2025-02-22 03:12:07 +0900
tag     : 
toc     : true
public  : true
parent  : [[/solana]] 
latex   : false
resource: 152083B3-D02C-4804-8AF1-2F5EE390D630
---
* TOC
{:toc}

# Solana: A new architecture for a high performance blockchain v0.8.13
> **저자**: Anatoly Yakovenko  
> **출처**: https://solana.com/solana-whitepaper.pdf   
> **발표 연도**: -  

---

### Table of Contents
- [Intro](#intro)
- [Network Design](#network-design)
- [Discussion](#discussion)
- [Further Reading](#further-reading)

---
### Intro
최근 솔라나의 이해도를 깊게 들어가고자 관련 논문을 찾아보던 중, 창업자 Anatoly가 작성한 백서를 발견했다. 어떤 아키텍처를 도입했기에 오늘날 하드웨어 성능으로 초당 710k의 트랜잭션 처리가 가능한지에 대해 나와있다. 기존 블록체인 노드는 본인 로컬 시간을 기준으로 트랜잭션을 처리하는데 블록체인 특성상 노드들이 다른 위치에 분산되어서 돌아간다 이때 각 노드들의 로컬 시간이 차이가 날 수 있어서 동일한 데이터라도 처리 결과에 영향을 준다는 의미다. 솔라나는 이 문제점들을 PoH를 중심으로 해결하며 성능을 높였다.

### Network Design

### Discussion
Anatoly는 퀄컴과 드롭박스에서 압축 기술과 HCP 특허를 가지고있고 CTO도 같은 퀄컴에서 메세지 전송 인프라일 경험이 솔라나에 그대로 묻어있는게 아닌가 생각된다. 
- 어떻게 PoH가 Byzantine Fault Tolerant를 줄여서 오버헤드를 줄이고 1초 안에 끝낼 수 있을까

### Further Reading
- Tendermint: Consensus without Mining
https://tendermint.com/static/docs/tendermint.pdf
- Hedera: A Governing Council & Public Hashgraph Network
https://s3.amazonaws.com/hedera-hashgraph/hh-whitepaper-v1.0-180313.pdf