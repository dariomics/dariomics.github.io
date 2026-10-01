---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign academic = site.data.academic %}

{% if academic %}
**Datos académicos encontrados.**
{% else %}
**No se encontraron datos académicos.**
{% endif %}

{% if academic.publications %}
**Archivo de publicaciones encontrado.**
{% else %}
**No se encontró el archivo de publicaciones.**
{% endif %}

{% assign publications = academic.publications.publications %}

{% if publications %}
**Número de publicaciones detectadas:** {{ publications.size }}
{% else %}
**No se detectaron publicaciones.**
{% endif %}
