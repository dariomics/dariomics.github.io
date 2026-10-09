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
  - Busca prioritariamente site.data.academic.publications.publications
    (correspondiente al archivo _data/academic/publications.yml)
  - Mantiene fallbacks para variaciones de nombres (publicaciones vs publications)
  ==============================================================================
{% endcomment %}
{% assign publications = site.data.academic.publications.publications | default: site.data.academic.publicaciones.publications | default: site.data.publicaciones.publications | default: site.data.publications.publications | default: site.data.academic.publications | default: site.data.academic.publicaciones %}

{% if publications and publications != empty %}

**Número de publicaciones: {{ publications.size }}**

{% comment %}
  ==============================================================================
  2. MAPPING ESTÁNDAR DE TIPOS DE PUBLICACIÓN Y TÍTULOS EN ESPAÑOL
  - Mantiene la categorización y orden temático predefinido por el usuario
  ==============================================================================
{% endcomment %}
{% assign section_types = "article,guideline,review,editorial,letter,preprint,chapter,poster,figure,other" | split: "," %}
{% assign section_titles = "Artículos,Guías y declaraciones,Revisiones,Editoriales,Cartas y respuestas,Preprints,Capítulos,Pósteres,Figuras,Otros productos" | split: "," %}

{% comment %}
  ==============================================================================
  3. DETECCIÓN DINÁMICA DE CATEGORÍAS ADICIONALES (Extensibilidad)
  - Captura cualquier valor de "type" presente en el YAML que no esté en la lista
    estándar para asegurar que no se oculte ninguna nueva categoría en el futuro
  ==============================================================================
{% endcomment %}
{% assign detected_types = publications | map: "type" | uniq %}
{% assign all_section_types = section_types %}

{% for d_type in detected_types %}
  {% unless section_types contains d_type %}
    {% assign all_section_types = all_section_types | push: d_type %}
  {% endunless %}
{% endfor %}

{% comment %}
  ==============================================================================
  4. ITERACIÓN Y RENDERIZADO DE SECCIONES
  ==============================================================================
{% endcomment %}
{% for section_type in all_section_types %}

  {% comment %} Conteo preventivo de productos por categoría {% endcomment %}
  {% assign section_count = 0 %}
  {% for publication in publications %}
    {% if publication.type == section_type %}
      {% assign section_count = section_count | plus: 1 %}
    {% endif %}
  {% endfor %}

  {% if section_count > 0 %}

---

  {% comment %} Determinación del título de la sección (mapeado o formateo dinámico) {% endcomment %}
  {% assign current_title = "" %}
  {% if section_types contains section_type %}
    {% for st in section_types %}
      {% if st == section_type %}
        {% assign current_title = section_titles[forloop.index0] %}
      {% endif %}
    {% endfor %}
  {% else %}
    {% assign current_title = section_type | replace: "_", " " | capitalize %}
  {% endif %}

## {{ current_title }} ({{ section_count }})

  {% comment %} Ordenamiento cronológico descendente (año más reciente a más antiguo) {% endcomment %}
  {% assign section_publications = publications | where: "type", section_type | sort: "year" | reverse %}

  {% for publication in section_publications %}

### {{ publication.title }}

{% comment %}
  ------------------------------------------------------------------------------
  A) LISTA DE AUTORES
  - Bolding automático para "José Darío Martínez-Ezquerro" y variantes
  - Limpieza defensiva contra puntos dobles (..)
  ------------------------------------------------------------------------------
{% endcomment %}
{% if publication.authors and publication.authors != empty %}
{{ publication.authors | join: ", " | replace: "José Darío Martínez-Ezquerro", "**José Darío Martínez-Ezquerro**" | replace: "Martínez-Ezquerro, José Darío", "**Martínez-Ezquerro, José Darío**" | append: "." | replace: "..", "." }}
{% endif %}

{% comment %}
  ------------------------------------------------------------------------------
  B) CITACIÓN SEGÚN EL TIPO DE PRODUCTO
  - Capítulos: Formato enriquecido (En: Editores, Libro, Páginas, Editorial, Año, ISBN)
  - Revistas / Libros / Fallback genérico por Año
  ------------------------------------------------------------------------------
{% endcomment %}
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

{% comment %}
  ------------------------------------------------------------------------------
  C) IDENTIFICADOR DIGITAL (DOI)
  ------------------------------------------------------------------------------
{% endcomment %}
{% if publication.doi and publication.doi != "" %}
doi: {{ publication.doi }}.
{% endif %}

{% comment %}
  ------------------------------------------------------------------------------
  D) ENLACE EXTERNO A LA PUBLICACIÓN
  ------------------------------------------------------------------------------
{% endcomment %}
{% if publication.url and publication.url != "" %}
[Consultar publicación]({{ publication.url }})
{% endif %}

{% comment %}
  ------------------------------------------------------------------------------
  E) TESIS ASOCIADA O DERIVADA
  ------------------------------------------------------------------------------
{% endcomment %}
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
