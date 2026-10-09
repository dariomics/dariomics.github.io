---
layout: default
title: Publicaciones Científicas
permalink: /publicaciones/
---

# Publicaciones Científicas

Artículos indizados, preprints, capítulos de libro, revisiones y notas científicas desarrolladas por nuestro equipo.

{% comment %}
  ==============================================================================
  1. CARGA MULTI-RUTA DEFENSIVA (Soporta _data/academic/ y _data/ directo)
  ==============================================================================
{% endcomment %}
{% assign raw_data = site.data.academic.publicaciones | default: site.data.publicaciones %}
{% assign items = raw_data.publications | default: raw_data.publicaciones | default: raw_data %}

{% if items and items != empty and items.size > 0 %}

**Número total de productos de difusión: {{ items.size }}**

{% comment %}
  ==============================================================================
  2. DETECCIÓN DINÁMICA DE TIPOS
  ==============================================================================
{% endcomment %}
{% assign detected_types = items | map: "type" | uniq %}

{% assign known_types = "article,preprint,chapter,review,editorial,letter,figure,other" | split: "," %}
{% assign known_titles = "Artículos científicos indizados,Preprints y documentos de trabajo,Capítulos de libro,Revisiones y estados del arte,Editoriales y notas del editor,Cartas al editor y réplicas,Figuras y datos científicos,Otros productos de difusión" | split: "," %}

{% assign active_types = "" | split: "" %}
{% for k_type in known_types %}
  {% if detected_types contains k_type %}
    {% assign active_types = active_types | push: k_type %}
  {% endif %}
{% endfor %}

{% for d_type in detected_types %}
  {% unless known_types contains d_type %}
    {% assign active_types = active_types | push: d_type %}
  {% endunless %}
{% endfor %}

{% comment %}
  ==============================================================================
  3. RENDERIZADO DE SECCIONES
  ==============================================================================
{% endcomment %}
{% for current_type in active_types %}

  {% assign section_items = items | where: "type", current_type | sort: "year" | reverse %}
  {% assign section_count = section_items.size %}

  {% if section_count > 0 %}

    {% assign section_title = "" %}
    {% if known_types contains current_type %}
      {% for k_type in known_types %}
        {% if k_type == current_type %}
          {% assign section_title = known_titles[forloop.index0] %}
        {% endif %}
      {% endfor %}
    {% else %}
      {% assign section_title = current_type | replace: "_", " " | capitalize %}
    {% endif %}

---

## {{ section_title }} ({{ section_count }})

    {% for item in section_items %}

### {{ item.title }}

{% if item.authors and item.authors != empty %}
**Autores:** {{ item.authors | join: ", " | replace: "José Darío Martínez-Ezquerro", "**José Darío Martínez-Ezquerro**" | replace: "Martínez-Ezquerro, José Darío", "**Martínez-Ezquerro, José Darío**" | append: "." | replace: "..", "." }}
{% endif %}

{% assign pub_medium = item.journal | default: item.publisher | default: item.book_title %}

{% if item.type == "article" or item.type == "review" or item.type == "editorial" or item.type == "letter" %}
  {% if pub_medium and pub_medium != "" %}**Revista:** {{ pub_medium }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}

{% elsif item.type == "preprint" %}
  {% if pub_medium and pub_medium != "" %}**Servidor de preprints:** {{ pub_medium }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}

{% elsif item.type == "chapter" %}
  {% assign b_title = item.book_title | default: item.journal %}
  En:{% if item.editors and item.editors != "" %} {{ item.editors }}{% endif %}{% if b_title and b_title != "" %} *{{ b_title }}*{% endif %}{% if item.pages and item.pages != "" %}, pp. {{ item.pages }}{% endif %}.{% if item.publisher and item.publisher != "" %} {{ item.publisher }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}{% if item.isbn and item.isbn != "" %} ISBN: {{ item.isbn }}.{% endif %}

{% elsif item.type == "figure" %}
  {% if pub_medium and pub_medium != "" %}**Repositorio:** {{ pub_medium }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}

{% else %}
  {% if pub_medium and pub_medium != "" %}**Publicación:** {{ pub_medium }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}
{% endif %}

{% if item.doi and item.doi != "" %}
doi: {{ item.doi }}.
{% endif %}

{% if item.related_thesis and item.related_thesis != "" %}
*Tesis relacionada:* {{ item.related_thesis }}
{% endif %}

{% if item.links and item.links != empty %}
  {% for link in item.links %}
[{{ link.label | default: "Ver enlace / publicación" }}]({{ link.url }}){% unless forloop.last %} | {% endunless %}
  {% endfor %}
{% elsif item.url and item.url != "" %}
[Ver enlace / publicación]({{ item.url }})
{% endif %}

<br>

    {% endfor %}

  {% endif %}

{% endfor %}

{% else %}

No hay publicaciones registradas.

{% endif %}
