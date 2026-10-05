---
layout: default
title: Programas de Servicio Social
permalink: /programas/
---

# Programas de Servicio Social

Conoce los programas disponibles, sus áreas de formación e investigación, y los proyectos desarrollados por nuestros estudiantes.

{% assign programs = site.data.service_social.programs %}
{% assign participations = site.data.academic.participations %}
{% assign people = site.data.people %}

{% for program in programs %}
<section markdown="1" style="margin-top: 3rem; margin-bottom: 4.5rem; padding-bottom: 2.5rem; border-bottom: 2px solid #e0e0e0;">

## {{ program.title }}

{% if program.description and program.description != "" %}
{{ program.description }}
{% endif %}

{% if program.areas %}
**Áreas de conocimiento:** {{ program.areas | join: ", " }}
{% endif %}

{% assign program_participations = participations | where: "program", program.id %}

### Estudiantes y Proyectos

{% if program_participations.size > 0 %}
{% for participation in program_participations %}{% assign person = people | where: "id", participation.person | first %}{% if person and person.public %}{% assign end_two = participation.end | slice: 0, 2 %}{% assign start_two = participation.start | slice: 0, 2 %}{% if end_two == "20" or end_two == "19" %}{% assign year_label = participation.end | slice: 0, 4 %}{% elsif start_two == "20" or start_two == "19" %}{% assign year_label = participation.start | slice: 0, 4 %}{% else %}{% assign year_label = site.time | date: "%Y" %}{% endif %}* {{ person.name }} ({{ year_label }}).{% if participation.project and participation.project != "" %} **{{ participation.project }}**.{% endif %}
{% endif %}{% endfor %}
{% else %}

*No hay estudiantes registrados en este programa actualmente.*

{% endif %}

</section>
{% endfor %}
