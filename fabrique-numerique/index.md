---
title: Fabrique numérique
---

### Les projets de la première saison

{% assign startups = site.startup %}
{% for startup in startups %}
* [{{ startup.title }}]({{ startup.url }}) 
> ##### {{ startup.mission }}
{% endfor %}
* [Bail confiance](./)
* [Co-construisons](./)
* [A Dock](./)
* [Assec](./)
