---
layout: default
title: Divulgación Científica
permalink: /divulgacion/
---

# Divulgación Científica

Artículos, infografías y materiales de comunicación pública de la ciencia desarrollados por nuestro equipo y estudiantes.

{% assign raw_data = site.data.academic.divulgacion %}
{% assign items = raw_data.divulgacion | default: raw_data %}

{% if items and items != empty %}

**Número de productos: {{ items.size }}**

{% assign section_types = "article,platform,infographic,event,other" | split: "," %}
{% assign section_titles = "Artículos de divulgación,Plataformas y portales web,Infografías y material gráfico,Eventos y proyectos,Otros materiales" | split: "," %}

{% for section_type in section_types %}

  {% assign section_count = 0 %}

  {% for item in items %}
    {% if item.type == section_type %}
      {% assign section_count = section_count | plus: 1 %}
    {% endif %}
  {% endfor %}

  {% if section_count > 0 %}

---

## {{ section_titles[forloop.index0] }} ({{ section_count }})

  {% assign section_items = items | where: "type", section_type | sort: "year" | reverse %}

  {% for item in section_items %}

### {{ item.title }}

{% if item.authors and item.authors != empty %}
**Autores:** {{ item.authors | join: ", " | replace: "José Darío Martínez-Ezquerro", "**José Darío Martínez-Ezquerro**" | replace: "Martínez-Ezquerro, José Darío", "**Martínez-Ezquerro, José Darío**" }}.
{% endif %}

{% assign pub_medium = item.journal | default: item.publisher | default: item.publication %}
{% if pub_medium and pub_medium != "" %}
**Plataforma / Medio:** {{ pub_medium }}.{% if item.year %} {{ item.year }}.{% endif %}
{% elsif item.year %}
**Año:** {{ item.year }}.
{% endif %}

{% if item.description and item.description != "" %}
{{ item.description }}
{% endif %}

{% if item.doi and item.doi != "" %}
doi: {{ item.doi }}.
{% endif %}

{% if item.url and item.url != "" %}
[Ver enlace / publicación]({{ item.url }})
{% endif %}

<br>

  {% endfor %}

  {% endif %}

{% endfor %}

{% else %}

No hay productos de divulgación científica registrados.

{% endif %}
