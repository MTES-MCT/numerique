---
title: Geek-lunch
---



Les Geek-lunch des ministères de la Transition écologique et solidaire et de la Cohésion des territoires : nos [Brown bag lunch](https://en.wikipedia.org/wiki/Packed_lunch) avec un invité, un problème, une réponse par la mise en oeuvre pratique d'une solution technique.

{% assign curDate = site.time | date: '%s' %}


### A venir

<ul>
  {% for post in site.categories.geek-lunch %}
  {% assign postStartDate = post.date | date: '%s' %}
    {% if postStartDate >= curDate %}
    <li>
      {{ post.date | date_to_string }} [{{ post.title }}]({{ post.url }}) par {{ post.speaker }}
    </li>
    {% endif %}
  {% endfor %}
</ul>

### Passés

<ul>
  {% for post in site.categories.geek-lunch %}
  {% assign postStartDate = post.date | date: '%s' %}
    {% if postStartDate < curDate %}
    <li>
      {{ post.date | date_to_string }} <a href="{{ post.url }}">{{ post.title }}</a> par {{ post.speaker }}
    </li>
    {% endif %}
  {% endfor %}
</ul>

<!---
Pour mémoire

- Nathann Cohen
- Machine Learning - Luc Mathis
- Git/Github - Julien Bouquillon
- Christian Quest
- API - Samuel Goldszmidt
- Gephi
- R réseaux sociaux - Stéphane Trainel
-->