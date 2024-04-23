---
title: I nostri candidati
layout: page
---
<ul class="candidati">
{% for candidato in site.data.candidati %}
  <li>
    <picture><a href="/candidati/{{candidato.slug}}"><img src="/assets/images/{{ candidato.slug }}.jpeg"></a></picture>
    <a href="/candidati/{{candidato.slug}}">{{ candidato.name }}</a>
  </li>
{% endfor %}
</ul>