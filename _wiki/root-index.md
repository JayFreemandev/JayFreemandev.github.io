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
    * [[/book/math-think]]
    * [[/book/python-clean-code]]
    * [[/book/think-about-think]]
    * [[/book/mark-wizard]]
    * [[/book/react-intro]]

* [[/quant]]
    * [[/quant/test1]]
    * [[/quant/test2]]
    * [[/quant/test3]]

* [[/finance]]
    * [[/finance/test1]]
    * [[/finance/test2]]
    * [[/finance/test3]]

* [[/math]]
    * [[/math/test1]]
    * [[/math/test2]]
    * [[/math/test3]]

* [[/article]]
    * [[/article/test1]]

* [[/system-deisgn]]
    * [[/system-deisgn/test1]]
    * [[/system-deisgn/test2]]
    * [[/system-deisgn/test3]]

* [[/programming]]
    * [[/programming/python]]
    * [[/programming/design-pattern]]
    * [[/programming/oop]]
    * [[/programming/effective-test]]

## Archive

* Memo
    * [[/2022]]
    * [[/2023]]
    * [[/2024]]

* [[/links]]
    * [[/links/2022]]
    * [[/links/2023]]
    * [[/links/2024]]

* [[/review]]
    * [[/review/2022]]
    * [[/review/2023]]
    * [[/review/2024]]

---

## blog posts
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

