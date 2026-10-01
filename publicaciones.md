---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications %}

Número de publicaciones: {{ publications.size }}

{% for publication in publications %}
## {{ publication.title }}

{{ publication.year }}

{% endfor %}
