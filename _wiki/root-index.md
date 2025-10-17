---
layout  : wikiindex
title   : wiki
toc     : true
public  : true
comment : false
updated : 2025-08-28 20:18:53 +0900
regenerate: true
---
## [[/project]] 
- Relative Strength Screener(KOSPI/KOSDAQ/NASDAQ)
- Short Momentum Nasdaq Screener
- Bitcoin Whale Transaction Detect
- Spitfire Systematic Trading
- [[/trading_asset_management]]

## [[/monad]] 
- [[/monad/txs]]


## [[/solana]]
- [[/solana/architecture]]

---

### [[/algorithms_data_structures]]
- Arrays & Strings
- Trees & Graphs
- Sorting & Searching
- Dynamic Programming
- Number Theory
- [[/programming/sql]]

### [[/system_design]]
### [[/system_behavior]]
### [[/live]] 

---

## [[/math]]
- [[/math/gcd]]
- [[/math/standard-deviation]]
- [[/math/time-weighted-return]]
- [[/math/intersections-of-equations]]

## [[/quant]]
- [[/quant/petrocurrency]] 
- [[/quant/pension]]
- [[/quant/volatility]]
- [[/quant/single-price-auction-call]]

## [[/languages]]
- [[/programming]]
    - [[/programming/python]]
    - [[/programming/rust]]
- Human
    - [[/languages/english]]
    - [[/languages/deutsch]]
    
## [[/summary]]
- [[/summary/how-to-break-goldman-sachs]]
- [[/summary/persona]]

## [[/lifehack]]
- [[/lifehack/health]]
- [[/lifehack/paper]]

## Archive
- [[/memo]]
    - [[/memo/2024]]
    - [[/memo/2025]]
    
- [[/links]]
    - [[/links/2024]]
    - [[/links/2025]]

- [[/review]]
    - [[/review/2022]]
    - [[/review/2023]]
    - [[/review/2024]]
    - [[/review/2025]]

---
<div>
    <ul>
{% for post in site.posts %}
    {% if post.public == true %}
        <li>
            <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">
                {{ post.title }}
            </a>
        </li>
    {% endif %}
{% endfor %}
    </ul>
</div>

