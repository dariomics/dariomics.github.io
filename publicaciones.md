---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign academic = site.data.academic.publications %}

## Prueba de estructura

{% for item in academic %}
- **Clave:** {{ item[0] }}
- **Valor:** {{ item[1] }}
{% endfor %}
