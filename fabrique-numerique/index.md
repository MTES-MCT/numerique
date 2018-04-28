---
title: Fabrique numérique
---

## Les projets de la première saison

En étroite collaboration avec [beta.gouv.fr](https://beta.gouv.fr/)


{% assign startups = site.startup %}
{% for startup in startups %}
### [{{ startup.title }}]({{ startup.url | prepend: site.baseurl }}) 
{{ startup.mission }}
Agent intrapreneur : <a href="mailto:{{ startup.contact }}">{{ startup.contact }}</a>
{% endfor %}
