---
layout  : wikiindex
title   : wiki
toc     : true
public  : true
comment : false
updated : 2023-12-17 14:46:01 +0900
regenerate: true
---
##### [[/quant]] 
- [[/quant/petrocurrency]] 

##### [[/solana]]
- [[/solana/architecture]]

##### [[/math]]
- [[/math/gcd]]
- [[/math/standard-deviation]]
- [[/math/time-weighted-return]]
- [[/math/intersections-of-equations]]

##### [[/programming]]
- [[/programming/python]]
- [[/programming/rust]]
- [[/programming/sql]]
- [[/programming/system-design]]

##### [[/infra]]
- [[/infra/kubernetes]]

##### [[/finance]]
- [[/finance/pension]]
- [[/finance/volatility]]
- [[/finance/single-price-auction-call]]

##### [[/summary]]
- [[/summary/how-to-break-goldman-sache]]
- [[/summary/persona]]
- [[/summary/20-percent-project]]

##### [[/lifehack]]
- [[/lifehack/health]]
- [[/lifehack/paper]]
- [[/lifehack/productivity]]

##### Archive
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

