---
layout: default
title: Divulgación
permalink: /divulgacion/
---

# Divulgación Científica

Artículos, infografías y materiales de comunicación pública de la ciencia desarrollados por nuestro equipo y estudiantes.

{% assign products = site.data.academic.products %}

{% assign divulgacion_items = "" | split: "" %}
{% for product in products %}
  {% if product.type == "divulgacion" or product.category == "divulgacion" %}
    {% assign divulgacion_items = divulgacion_items | push: product %}
  {% endif %}
{% endfor %}

{% if divulgacion_items.size > 0 %}
<section markdown="1" style="margin-top: 2.5rem; margin-bottom: 4rem;">

{% for item in divulgacion_items %}
### {{ item.title }}

{% if item.authors %}
**Autores:** {{ item.authors | join: ", " }}
{% endif %}

{% if item.journal or item.publisher %}
**Publicación:** {{ item.journal }}{{ item.publisher }}
{% endif %}

{% if item.year %}
**Año:** {{ item.year }}
{% endif %}

{% if item.description and item.description != "" %}
{{ item.description }}
{% endif %}

{% if item.doi or item.url %}
{% assign link = item.url %}
{% if item.doi %}
  {% assign link = "https://doi.org/" | append: item.doi %}
{% endif %}
[Ver publicación]({{ link }})
{% endif %}

---
{% endfor %}

</section>
{% else %}

*No hay publicaciones de divulgación registradas actualmente.*

{% endif %}
