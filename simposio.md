---
layout: default
title: Simposio Internacional sobre Cognición Sensorial
permalink: /simposio/
---

Plataforma oficial que alberga las ediciones anuales del **Simposio Internacional sobre Cognición Sensorial** (2020 a la fecha). Incluye los programas académicos, memorias de resúmenes, ponencias y grabaciones (sección en desarrollo).

El Simposio Internacional sobre Cognición Sensorial es un espacio de encuentro, diálogo y **apropiación social del conocimiento** en torno a la cognición y los sistemas sensoriales. Es un foro de **acceso abierto** que reúne a investigadores, estudiantes, profesionales y personas interesadas en explorar cómo construimos nuestra experiencia del mundo a través de los sentidos.

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
