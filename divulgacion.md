---
layout: default
title: Divulgación Científica
permalink: /divulgacion/
---

Artículos, infografías y materiales de comunicación pública de la ciencia desarrollados por nuestro equipo y estudiantes.

<br>

{% assign items = site.data.academic.divulgacion %}

{% if items == nil or items.size == 0 %}
  {% assign items = site.data.divulgacion %}
{% endif %}

{% if items == nil or items.size == 0 %}
  {% assign items = site.data.academic.products | where: "type", "divulgacion" %}
{% endif %}

{% if items == nil or items.size == 0 %}
  {% assign items = page.divulgacion_list %}
{% endif %}

{% if items and items.size > 0 %}
{% for item in items %}

### {{ item.title }}

{% if item.authors %}
**Autores:** {{ item.authors | join: ", " }}
{% endif %}

{% if item.journal %}
**Publicación:** {{ item.journal }}
{% elsif item.publisher %}
**Plataforma / Medio:** {{ item.publisher }}
{% endif %}

{% if item.year %}
**Año:** {{ item.year }}
{% endif %}

{% if item.description and item.description != "" %}
{{ item.description }}
{% endif %}

{% if item.doi or item.url %}
  {% assign link = item.url %}
  {% if item.doi and item.doi != "" %}
    {% assign link = "https://doi.org/" | append: item.doi %}
  {% endif %}
[Ver enlace / publicación]({{ link }})
{% endif %}

<br>

---

<br>

{% endfor %}
{% else %}

*No hay publicaciones de divulgación registradas actualmente.*

{% endif %}
