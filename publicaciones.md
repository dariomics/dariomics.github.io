---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% comment %}
  ==============================================================================
  1. CARGA MULTI-RUTA DE DATOS (Resiliente y defensiva)
  - Prioriza site.data.academic.publications.publications
  - Incluye fallbacks seguros para cualquier variación de nombres de archivos
  ==============================================================================
{% endcomment %}
{% assign publications = site.data.academic.publications.publications | default: site.data.academic.publicaciones.publications | default: site.data.publicaciones.publications | default: site.data.publications.publications | default: site.data.academic.publications | default: site.data.academic.publicaciones %}

{% if publications and publications != empty %}

**Número total de productos de difusión: {{ publications.size }}**

{% comment %}
  ==============================================================================
  2. CLASIFICACIÓN DE TIPOS INDIZADOS Y OTRAS CATEGORÍAS
  ==============================================================================
{% endcomment %}
{% assign indexed_types = "article,guideline,review,editorial,letter" | split: "," %}
{% assign indexed_titles = "Artículos originales,Guías y declaraciones,Revisiones,Editoriales,Cartas y respuestas" | split: "," %}

{% assign other_types = "preprint,chapter,poster,figure,other" | split: "," %}
{% assign other_titles = "Preprints y documentos de trabajo,Capítulos de libro,Pósteres en congresos,Figuras y datos científicos,Otros productos" | split: "," %}

{% comment %}
  ==============================================================================
  3. BLOQUE MACRO: PUBLICACIONES EN REVISTAS INDIZADAS
  - Suma acumulativa de article, guideline, review, editorial y letter
  - Desglose jerárquico interno mantenido con sus subtotales
  ==============================================================================
{% endcomment %}
{% assign indexed_total = 0 %}
{% for pub in publications %}
  {% if indexed_types contains pub.type %}
    {% assign indexed_total = indexed_total | plus: 1 %}
  {% endif %}
{% endfor %}

{% if indexed_total > 0 %}

---

## Publicaciones en revistas indizadas ({{ indexed_total }})

  {% for ind_type in indexed_types %}
    {% assign sub_publications = publications | where: "type", ind_type | sort: "year" | reverse %}
    {% assign sub_count = sub_publications.size %}

    {% if sub_count > 0 %}

      {% assign sub_title = indexed_titles[forloop.index0] %}

### {{ sub_title }} ({{ sub_count }})

      {% for publication in sub_publications %}

#### {{ publication.title }}

{% comment %} Autoría y resaltado de firma principal {% endcomment %}
{% if publication.authors and publication.authors != empty %}
{{ publication.authors | join: ", " | replace: "José Darío Martínez-Ezquerro", "**José Darío Martínez-Ezquerro**" | replace: "Martínez-Ezquerro, José Darío", "**Martínez-Ezquerro, José Darío**" | append: "." | replace: "..", "." }}
{% endif %}

{% comment %} Medio / Revista / Libro / Año {% endcomment %}
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

{% comment %} Metadatos adicionales y enlaces {% endcomment %}
{% if publication.doi and publication.doi != "" %}
doi: {{ publication.doi }}.
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

{% endif %}

{% comment %}
  ==============================================================================
  4. BLOQUE MACRO: OTRAS CATEGORÍAS INDEPENDIENTES
  - Renderizado autónomo de Preprints, Capítulos, Pósteres, Figuras, etc.
  - Detección dinámica de tipos no contemplados para evitar ocultamiento de datos
  ==============================================================================
{% endcomment %}
{% assign all_known = indexed_types | concat: other_types %}
{% assign detected_types = publications | map: "type" | uniq %}
{% assign remaining_types = other_types %}

{% for d_type in detected_types %}
  {% unless all_known contains d_type %}
    {% assign remaining_types = remaining_types | push: d_type %}
  {% endunless %}
{% endfor %}

{% for sec_type in remaining_types %}
  {% assign sec_publications = publications | where: "type", sec_type | sort: "year" | reverse %}
  {% assign sec_count = sec_publications.size %}

  {% if sec_count > 0 %}

---

    {% assign sec_title = "" %}
    {% if other_types contains sec_type %}
      {% for ot in other_types %}
        {% if ot == sec_type %}
          {% assign sec_title = other_titles[forloop.index0] %}
        {% endif %}
      {% endfor %}
    {% else %}
      {% assign sec_title = sec_type | replace: "_", " " | capitalize %}
    {% endif %}

## {{ sec_title }} ({{ sec_count }})

    {% for publication in sec_publications %}

### {{ publication.title }}

{% comment %} Autoría y resaltado de firma principal {% endcomment %}
{% if publication.authors and publication.authors != empty %}
{{ publication.authors | join: ", " | replace: "José Darío Martínez-Ezquerro", "**José Darío Martínez-Ezquerro**" | replace: "Martínez-Ezquerro, José Darío", "**Martínez-Ezquerro, José Darío**" | append: "." | replace: "..", "." }}
{% endif %}

{% comment %} Medio / Revista / Libro / Año {% endcomment %}
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

{% comment %} Metadatos adicionales y enlaces {% endcomment %}
{% if publication.doi and publication.doi != "" %}
doi: {{ publication.doi }}.
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
