---
layout: default
title: 竞品动态
---
<h1>竞品动态</h1>
<p class="meta">每两周整理一次企业 / ERP AI 产品的公开发布。</p>

{% assign posts = site.pages | where_exp: "p", "p.path contains 'competitors/'" | where_exp: "p", "p.name != 'index.md'" | sort: "path" | reverse %}

{% if posts.size == 0 %}
<p class="empty">第一期将随下一期每周简报一起发布。</p>
{% else %}
<ul class="list">
{% for p in posts %}
  <li class="item">
    <a class="t" href="{{ p.url | relative_url }}">{{ p.title }}</a>
    <div class="meta">{{ p.date | date: "%Y-%m-%d" }}</div>
    {% if p.summary %}<p>{{ p.summary }}</p>{% endif %}
  </li>
{% endfor %}
</ul>
{% endif %}
