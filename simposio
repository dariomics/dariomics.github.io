---
layout: default
title: Simposio Internacional sobre Cognición Sensorial
permalink: /simposio/
---

Plataforma oficial que alberga las ediciones anuales del Simposio Internacional sobre Cognición Sensorial (2020 a la fecha). Incluye los programas académicos, memorias de resúmenes, ponencias y grabaciones enfocadas en investigaciones sobre aspectos cognitivos de los sistemas sensoriales e interacciones multidisciplinarias.

<br>

{% assign items = site.data.academic.divulgacion | where: "publisher", "Sitio web del evento" %}

{% if items == nil or items.size == 0 %}
  {% assign items = site.data.academic.simposio %}
{% endif %}

{% if items and items.size > 0 %}
{% for item in items %}

### {{ item.title }}

{% if item.authors %}
**Autores / Coordinadores:** {{ item.authors | join: ", " }}
{% endif %}

{% if item.publisher %}
**Plataforma / Medio:** {{ item.publisher }}
{% endif %}

{% if item.year %}
**Año / Edición:** {{ item.year }}
{% endif %}

{% if item.description and item.description != "" %}
{{ item.description }}
{% endif %}

{% if item.url %}
[Acceder al Portal Oficial del Simposio]({{ item.url }})
{% endif %}

<br>

---

<br>

{% endfor %}
{% else %}

*Información y recursos del simposio en actualización.*

{% endif %}
