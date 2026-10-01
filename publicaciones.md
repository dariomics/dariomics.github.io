---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications %}

{% assign has_guidelines = false %}
{% assign has_articles = false %}
{% assign has_reviews = false %}
{% assign has_editorials = false %}
{% assign has_letters = false %}
{% assign has_preprints = false %}
{% assign has_chapters = false %}
{% assign has_posters = false %}
{% assign has_figures = false %}
{% assign has_other = false %}

{% for publication in publications %}
  {% if publication.type == "guideline" %}
    {% assign has_guidelines = true %}
  {% elsif publication.type == "article" %}
    {% assign has_articles = true %}
  {% elsif publication.type == "review" %}
    {% assign has_reviews = true %}
  {% elsif publication.type == "editorial" %}
    {% assign has_editorials = true %}
  {% elsif publication.type == "letter" %}
    {% assign has_letters = true %}
  {% elsif publication.type == "preprint" %}
    {% assign has_preprints = true %}
  {% elsif publication.type == "chapter" %}
    {% assign has_chapters = true %}
  {% elsif publication.type == "poster" %}
    {% assign has_posters = true %}
  {% elsif publication.type == "figure" %}
    {% assign has_figures = true %}
  {% elsif publication.type == "other" %}
    {% assign has_other = true %}
  {% endif %}
{% endfor %}

{% if has_guidelines %}
## Guías y declaraciones

{% for publication in publications %}
  {% if publication.type == "guideline" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_articles %}
## Artículos

{% for publication in publications %}
  {% if publication.type == "article" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_reviews %}
## Revisiones

{% for publication in publications %}
  {% if publication.type == "review" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_editorials %}
## Editoriales

{% for publication in publications %}
  {% if publication.type == "editorial" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_letters %}
## Cartas al editor

{% for publication in publications %}
  {% if publication.type == "letter" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_preprints %}
## Preprints

{% for publication in publications %}
  {% if publication.type == "preprint" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista o servidor:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_chapters %}
## Capítulos

{% for publication in publications %}
  {% if publication.type == "chapter" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Libro o obra:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% elsif publication.url and publication.url != "" %}
**Enlace:** [{{ publication.url }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_posters %}
## Pósteres

{% for publication in publications %}
  {% if publication.type == "poster" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista o plataforma:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_figures %}
## Figuras y productos gráficos

{% for publication in publications %}
  {% if publication.type == "figure" %}

### {{ publication.title }}

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% elsif publication.url and publication.url != "" %}
**Enlace:** [{{ publication.url }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
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

**Año:** {{ publication.year }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Publicación:** {{ publication.journal }}
{% endif %}

{% if publication.doi and publication.doi != "" %}
**DOI:** [{{ publication.doi }}]({{ publication.url }})
{% elsif publication.url and publication.url != "" %}
**Enlace:** [{{ publication.url }}]({{ publication.url }})
{% endif %}

{% if publication.sources and publication.sources != empty %}
**Fuentes:** {{ publication.sources | join: ", " }}
{% endif %}

{% if publication.related_thesis and publication.related_thesis != "" %}
**Tesis relacionada:** {{ publication.related_thesis }}
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}
