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


##### [[/programming]]
* [[/programming/python]]
    * [[/programming/python/test]]
* [[/programming/design-pattern]]
* [[/programming/oop]]
* [[/programming/effective-test]]
* [[/programming/sql]]
* [[/programming/system-deisgn]]
    * [[/programming/system-deisgn/test]]  

##### [[/math]]
* [[/math/gcd]]
* [[/math/standard-deviation]]
* [[/math/time-weighted-return]]

##### [[/finance]]
* [[/finance/pension]]
* [[/finance/volatility]]
* [[/finance/single-price-auction-call]]

##### [[/crypto]]
* [[/crypto/pixels]]
   * [[/crypto/pixels/journey]] 


##### [[/summary]]
* [[/summary/how-to-break-goldman-sache]]
* [[/summary/persona]]
* [[/summary/20-percent-project]]




##### [[/lifehack]]
* [[/lifehack/health]]
* [[/lifehack/paper]]


##### Archive
* [[/book]]
    * [[/book/2024]]

* [[memo]]
    * [[/memo/2024]]

* [[/links]]
    * [[/links/2024]]

* [[/review]]
    * [[/review/2022]]
    * [[/review/2023]]
    * [[/review/2024]]

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

