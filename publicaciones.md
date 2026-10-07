---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications | default: site.data.publicaciones.publications %}

{% if publications and publications != empty %}

**Número de publicaciones: {{ publications.size }}**

{% assign section_types = "article,guideline,review,editorial,letter,preprint,chapter,poster,figure,other" | split: "," %}
{% assign section_titles = "Artículos,Guías y declaraciones,Revisiones,Editoriales,Cartas y respuestas,Preprints,Capítulos,Pósteres,Figuras,Otros productos" | split: "," %}

{% for section_type in section_types %}

  {% assign section_count = 0 %}

  {% for publication in publications %}
    {% if publication.type == section_type %}
      {% assign section_count = section_count | plus: 1 %}
    {% endif %}
  {% endfor %}

  {% if section_count > 0 %}

---

## {{ section_titles[forloop.index0] }} ({{ section_count }})

  {% assign section_publications = publications | where: "type", section_type | sort: "year" | reverse %}

  {% for publication in section_publications %}

### {{ publication.title }}

{% if publication.authors and publication.authors != empty %}
{{ publication.authors | join: ", " | replace: "José Darío Martínez-Ezquerro", "**José Darío Martínez-Ezquerro**" }}.
{% endif %}

{% if publication.type == "chapter" %}
  {% assign b_title = publication.book_title | default: publication.book | default: publication.journal %}
  En:{% if publication.editors and publication.editors != "" %} {{ publication.editors }}{% endif %}{% if b_title and b_title != "" %} *{{ b_title }}*{% endif %}{% if publication.pages and publication.pages != "" %}, pp. {{ publication.pages }}{% endif %}.{% if publication.publisher and publication.publisher != "" %} {{ publication.publisher }}.{% endif %}{% if publication.year %} {{ publication.year }}.{% endif %}{% if publication.isbn and publication.isbn != "" %} ISBN: {{ publication.isbn }}.{% endif %}
{% elsif publication.journal and publication.journal != "" %}
  {{ publication.journal }}. {{ publication.year }}.
{% elsif publication.book and publication.book != "" %}
  {{ publication.book }}. {{ publication.year }}.
{% elsif publication.year %}
  {{ publication.year }}.
{% endif %}

{% if publication.doi and publication.doi != "" %}
doi:{{ publication.doi }}.
{% endif %}

{% if publication.url and publication.url != "" %}
[Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

<br>

  {% endfor %}

  {% endif %}

{% endfor %}

{% else %}

No hay publicaciones académicas registradas.

{% endif %}
