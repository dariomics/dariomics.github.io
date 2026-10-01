---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications %}

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

## {{ section_titles[forloop.index0] }} ({{ section_count }})

  {% assign section_publications = publications | where: "type", section_type | sort: "year" | reverse %}

  {% for publication in section_publications %}

### {{ publication.title }}

{% if publication.authors and publication.authors != empty %}
{{ publication.authors | join: ", " }}.
{% endif %}

{% if publication.journal and publication.journal != "" %}
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

  {% endfor %}

  {% endif %}

{% endfor %}

{% else %}

No hay publicaciones académicas registradas.

{% endif %}
