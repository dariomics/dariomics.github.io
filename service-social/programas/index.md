---
layout: default
title: Programas de Servicio Social
permalink: /service-social/programas/
---

# Programas de Servicio Social

Conoce los programas disponibles y sus áreas de formación e investigación.

{% assign programs = site.data.service_social.programs %}

{% for program in programs %}
## {{ program.title }}

{{ program.description }}

{% if program.areas %}
**Áreas:**

{% for area in program.areas %}
- {{ area }}
{% endfor %}
{% endif %}

{% if program.active %}
**Programa activo**
{% endif %}

---
{% endfor %}
