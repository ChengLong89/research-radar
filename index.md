---
layout: default
title: Research Radar
---
<h1>每周简报</h1>
<p class="meta">{{ site.description }}</p>

{% assign digests = site.pages | where_exp: "p", "p.path contains 'digests/'" | sort: "path" | reverse %}

<div class="chips" id="filters">
  <button class="chip on" data-topic="">全部</button>
  {% for pair in site.topic_labels %}<button class="chip" data-topic="{{ pair[0] }}">{{ pair[1] }}</button>{% endfor %}
</div>

{% if digests.size == 0 %}
<p class="empty">第一期将在本周日早上发布。</p>
{% else %}
<ul class="list" id="digests">
{% for p in digests %}
  <li class="item" data-topics="{{ p.topics | join: ' ' }}">
    <a class="t" href="{{ p.url | relative_url }}">{{ p.title }}</a>
    <div class="meta">{{ p.date | date: "%Y-%m-%d" }}</div>
    {% if p.summary %}<p>{{ p.summary }}</p>{% endif %}
    {% if p.topics %}<div class="chips">{% for t in p.topics %}<span class="chip">{{ site.topic_labels[t] | default: t }}</span>{% endfor %}</div>{% endif %}
  </li>
{% endfor %}
</ul>
{% endif %}

<script>
(function(){
  var btns=document.querySelectorAll('#filters button'),items=document.querySelectorAll('#digests .item');
  btns.forEach(function(b){b.addEventListener('click',function(){
    btns.forEach(function(x){x.classList.remove('on')});b.classList.add('on');
    var t=b.dataset.topic;
    items.forEach(function(i){i.style.display=(!t||(' '+i.dataset.topics+' ').indexOf(' '+t+' ')>-1)?'':'none'});
  })});
})();
</script>
