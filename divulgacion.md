---
layout: default
title: Divulgación Científica
permalink: /divulgacion/
---

# Divulgación Científica

Artículos, libros de divulgación, infografías, simposios, conferencias, pódcasts y recursos educativos desarrollados por nuestro equipo para la comunidad.

{% assign raw_data = site.data.academic.divulgacion %}
{% assign items = raw_data.divulgacion | default: raw_data %}

{% if items and items != empty %}

**Número de productos de divulgación: {{ items.size }}**

{% comment %}
  ==============================================================================
  1. DETECCIÓN DINÁMICA DE TIPOS PRESENTES EN LOS DATOS
  ==============================================================================
{% endcomment %}
{% assign detected_types = items | map: "type" | uniq %}

{% comment %}
  2. Mapeo de títulos preferenciales para la taxonomía estándar
{% endcomment %}
{% assign known_types = "article,book,chapter,infographic,event,presentation,media,platform,educational,software_tool,dataset_open,other" | split: "," %}
{% assign known_titles = "Artículos de divulgación,Libros de divulgación,Capítulos de divulgación,Infografías y material gráfico,Simposios y eventos de divulgación,Conferencias y charlas públicas,Medios y pódcasts,Plataformas y portales web,Materiales educativos y guías didácticas,Herramientas interactivas y aplicaciones,Recursos gráficos y bases abiertas,Otros materiales de divulgación" | split: "," %}

{% comment %}
  3. Ordenar: primero los conocidos en su orden preferente, luego cualquier tipo nuevo detectado
{% endcomment %}
{% assign active_types = "" | split: "" %}
{% for k_type in known_types %}
  {% if detected_types contains k_type %}
    {% assign active_types = active_types | push: k_type %}
  {% endif %}
{% endfor %}

{% for d_type in detected_types %}
  {% unless known_types contains d_type %}
    {% assign active_types = active_types | push: d_type %}
  {% endunless %}
{% endfor %}

{% comment %}
  ==============================================================================
  4. ITERACIÓN SOBRE TODOS LOS TIPOS ACTIVOS (ESTÁNDAR O NUEVOS)
  ==============================================================================
{% endcomment %}
{% for current_type in active_types %}

  {% assign section_items = items | where: "type", current_type | sort: "year" | reverse %}
  {% assign section_count = section_items.size %}

  {% if section_count > 0 %}

    {% comment %} Determinar el título de la sección (Búsqueda o Fallback automático) {% endcomment %}
    {% assign section_title = "" %}
    {% if known_types contains current_type %}
      {% for k_type in known_types %}
        {% if k_type == current_type %}
          {% assign section_title = known_titles[forloop.index0] %}
        {% endif %}
      {% endfor %}
    {% else %}
      {% comment %} Formato automático para tipos no registrados previamente {% endcomment %}
      {% assign section_title = current_type | replace: "_", " " | capitalize %}
    {% endif %}

---

## {{ section_title }} ({{ section_count }})

    {% for item in section_items %}

### {{ item.title }}

{% if item.authors and item.authors != empty %}
**Autores / Creadores:** {{ item.authors | join: ", " | replace: "José Darío Martínez-Ezquerro", "**José Darío Martínez-Ezquerro**" | replace: "Martínez-Ezquerro, José Darío", "**Martínez-Ezquerro, José Darío**" | append: "." | replace: "..", "." }}
{% endif %}

{% assign pub_medium = item.journal | default: item.publisher | default: item.event_name | default: item.publication %}

{% comment %} --- REGLAS DE PRESENTACIÓN SEGÚN EL TIPO --- {% endcomment %}

{% if item.type == "article" %}
  {% if pub_medium and pub_medium != "" %}**Revista:** {{ pub_medium }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}

{% elsif item.type == "book" %}
  {% if item.publisher and item.publisher != "" %}**Editorial:** {{ item.publisher }}.{% endif %}{% if item.pages and item.pages != "" %} ({{ item.pages }}).{% endif %}{% if item.year %} {{ item.year }}.{% endif %}{% if item.isbn and item.isbn != "" %} ISBN: {{ item.isbn }}.{% endif %}

{% elsif item.type == "chapter" %}
  {% assign b_title = item.book_title | default: item.journal %}
  En:{% if item.editors and item.editors != "" %} {{ item.editors }}{% endif %}{% if b_title and b_title != "" %} *{{ b_title }}*{% endif %}{% if item.pages and item.pages != "" %}, pp. {{ item.pages }}{% endif %}.{% if item.publisher and item.publisher != "" %} {{ item.publisher }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}{% if item.isbn and item.isbn != "" %} ISBN: {{ item.isbn }}.{% endif %}

{% elsif item.type == "event" %}
  {% if item.edition and item.edition != "" %}**Edición:** {{ item.edition }}. {% endif %}{% if pub_medium and pub_medium != "" %}**Evento:** {{ pub_medium }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}

{% elsif item.type == "platform" %}
  {% if pub_medium and pub_medium != "" %}**Plataforma / Sitio web:** {{ pub_medium }}.{% endif %}{% if item.year %} {{ item.year }}.{% endif %}

{% else %}
  {% comment %} REGLA DE FALLBACK GENERAL PARA CUALQUIER TIPO NUEVO O NO LISTADO {% endcomment %}
  {% if pub_medium and pub_medium != "" %}**Medio / Publicación:** {{ pub_medium }}.{% endif %}{% if item.format and item.format != "" %} ({{ item.format }}).{% endif %}{% if item.version and item.version != "" %} [{{ item.version }}].{% endif %}{% if item.year %} {{ item.year }}.{% endif %}{% if item.isbn and item.isbn != "" %} ISBN: {{ item.isbn }}.{% endif %}
{% endif %}

{% if item.description and item.description != "" %}
{{ item.description }}
{% endif %}

{% if item.doi and item.doi != "" %}
doi: {{ item.doi }}.
{% endif %}

{% if item.links and item.links != empty %}
  {% for link in item.links %}
[{{ link.label | default: "Ver enlace / publicación" }}]({{ link.url }}){% unless forloop.last %} | {% endunless %}
  {% endfor %}
{% elsif item.urls and item.urls != empty %}
  {% for u in item.urls %}
[Ver enlace {{ forloop.index }}]({{ u }}){% unless forloop.last %} | {% endunless %}
  {% endfor %}
{% elsif item.url and item.url != "" %}
[Ver enlace / publicación]({{ item.url }})
{% endif %}

<br>

    {% endfor %}

  {% endif %}

{% endfor %}

{% else %}

No hay productos de divulgación científica registrados.

{% endif %}
