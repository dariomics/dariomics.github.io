---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications %}

{% if publications and publications != empty %}

Número de publicaciones: {{ publications.size }}

{% assign publication_types = "guideline,article,review,editorial,letter,preprint,chapter,poster,figure,other" | split: "," %}

{% for type in publication_types %}

  {% assign type_publications = publications | where: "type", type %}

  {% if type_publications and type_publications != empty %}

## {% case type %}
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
{% endcase %}

    {% assign sorted_publications = type_publications | sort: "year" | reverse %}

    {% for publication in sorted_publications %}

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

  {% endif %}

{% endfor %}

{% else %}

No hay publicaciones académicas registradas.

{% endif %}
