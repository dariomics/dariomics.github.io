---
layout: default
title: Egresados
permalink: /egresados/
---

# Egresados

Personas que han concluido su participación en los programas de Servicio Social.

{% assign people = site.data.people %}
{% assign participations = site.data.service_social.participations %}
{% assign programs = site.data.service_social.programs %}

{% for participation in participations %}
  {% if participation.status == "completed" %}

    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person.public %}
## {{ person.name }}

**Programa:** {{ program.title }}

**Periodo:** {{ participation.start }} – {{ participation.end }}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products != empty %}
**Productos:** {{ participation.products | join: ", " }}
{% endif %}

---
    {% endif %}
  {% endif %}
{% endfor %}
