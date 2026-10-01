---
layout: default
title: Publicaciones
permalink: /publicaciones/
---

# Publicaciones

Publicaciones académicas y productos de investigación de Dariomics.

{% assign publications = site.data.academic.publications.publications %}

{% if publications and publications != empty %}

{% for publication in publications %}

### {{ publication.title }}

{% if publication.authors and publication.authors != empty %}
**Autores:**

{% for author in publication.authors %}
- {{ author }}
{% endfor %}
{% endif %}

{% if publication.year %}
**Año:** {{ publication.year }}
{% endif %}

{% if publication.type %}
**Tipo:** {{ publication.type }}
{% endif %}

{% if publication.journal and publication.journal != "" %}
**Revista:** {{ publication.journal }}
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

{% endfor %}

{% else %}

No hay publicaciones registradas.

{% endif %}
