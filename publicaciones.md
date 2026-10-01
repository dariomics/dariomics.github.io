---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications %}

{% assign has_guideline = false %}
{% assign has_article = false %}
{% assign has_review = false %}
{% assign has_editorial = false %}
{% assign has_letter = false %}
{% assign has_preprint = false %}
{% assign has_chapter = false %}
{% assign has_poster = false %}
{% assign has_figure = false %}
{% assign has_other = false %}

{% for publication in publications %}
  {% if publication.type == "guideline" %}
    {% assign has_guideline = true %}
  {% elsif publication.type == "article" %}
    {% assign has_article = true %}
  {% elsif publication.type == "review" %}
    {% assign has_review = true %}
  {% elsif publication.type == "editorial" %}
    {% assign has_editorial = true %}
  {% elsif publication.type == "letter" %}
    {% assign has_letter = true %}
  {% elsif publication.type == "preprint" %}
    {% assign has_preprint = true %}
  {% elsif publication.type == "chapter" %}
    {% assign has_chapter = true %}
  {% elsif publication.type == "poster" %}
    {% assign has_poster = true %}
  {% elsif publication.type == "figure" %}
    {% assign has_figure = true %}
  {% elsif publication.type == "other" %}
    {% assign has_other = true %}
  {% endif %}
{% endfor %}

{% if has_guideline %}
## Guías y declaraciones

{% for publication in publications %}
  {% if publication.type == "guideline" %}
### {{ publication.title }}

**Tipo:** Guía o declaración

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Revista o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_article %}
## Artículos

{% for publication in publications %}
  {% if publication.type == "article" %}
### {{ publication.title }}

**Tipo:** Artículo

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Revista o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_review %}
## Revisiones

{% for publication in publications %}
  {% if publication.type == "review" %}
### {{ publication.title }}

**Tipo:** Revisión

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Revista o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_editorial %}
## Editoriales

{% for publication in publications %}
  {% if publication.type == "editorial" %}
### {{ publication.title }}

**Tipo:** Editorial

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Revista o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_letter %}
## Cartas y respuestas

{% for publication in publications %}
  {% if publication.type == "letter" %}
### {{ publication.title }}

**Tipo:** Carta o respuesta

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Revista o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_preprint %}
## Preprints

{% for publication in publications %}
  {% if publication.type == "preprint" %}
### {{ publication.title }}

**Tipo:** Preprint

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Revista o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_chapter %}
## Capítulos

{% for publication in publications %}
  {% if publication.type == "chapter" %}
### {{ publication.title }}

**Tipo:** Capítulo

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Libro o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_poster %}
## Pósteres

{% for publication in publications %}
  {% if publication.type == "poster" %}
### {{ publication.title }}

**Tipo:** Póster

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.journal and publication.journal != "" %}
**Revista o fuente:** {{ publication.journal }}
{% endif %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_figure %}
## Figuras

{% for publication in publications %}
  {% if publication.type == "figure" %}
### {{ publication.title }}

**Tipo:** Figura

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_other %}
## Otros productos

{% for publication in publications %}
  {% if publication.type == "other" %}
### {{ publication.title }}

**Tipo:** Otro

**Año:** {{ publication.year }}

**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}

{% if publication.url and publication.url != "" %}
**Publicación:** [Consultar publicación]({{ publication.url }})
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}
