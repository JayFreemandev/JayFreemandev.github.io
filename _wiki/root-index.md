---
layout  : wikiindex
title   : wiki
toc     : true
public  : true
comment : false
updated : 2023-12-17 14:46:01 +0900
regenerate: true
---

## Wiki 

* [[/book]]
    * [[/book/2024]]

* [[/quant]]
    * [[/quant/how-to-break-goldman-sache]]

* [[/finance]]
    * [[/finance/pension]]

* [[/math]]
    * [[/math/gcd]]

* [[/system-deisgn]]
    * [[/system-deisgn/test1]]

* [[/programming]]
    * [[/programming/python]]
    * [[/programming/design-pattern]]
    * [[/programming/oop]]
    * [[/programming/effective-test]]

* [[/health]]

## Archive

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

