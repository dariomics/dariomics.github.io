---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications %}

{% if publications and publications != empty %}

## Publicaciones académicas

Número de publicaciones: {{ publications.size }}

{% assign current_type = "" %}

{% for publication in publications %}

  {% if publication.type != current_type %}

    {% assign current_type = publication.type %}

## {% case publication.type %}
{% when "guideline" %}Guías y declaraciones
{% when "article" %}Artículos
{% when "review" %}Revisiones
{% when "editorial" %}Editoriales
{% when "letter" %}Cartas y respuestas
{% when "preprint" %}Preprints
{% when "chapter" %}Capítulos
{% when "poster" %}Pósteres
{% when "figure" %}Figuras
{% when "other" %}Otros productos
{% else %}{{ publication.type | capitalize }}
{% endcase %}

  {% endif %}

### {{ publication.title }}

{% if publication.authors and publication.authors != empty %}
{% for author in publication.authors %}{{ author }}{% unless forloop.last %}, {% endunless %}{% endfor %}.
{% endif %}

{% if publication.journal and publication.journal != "" %}
{{ publication.journal }}. {{ publication.year }}.
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

{% else %}

No hay publicaciones académicas registradas.

{% endif %}
