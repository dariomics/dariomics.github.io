---
layout: default
title: Divulgación
permalink: /divulgacion/
---

# Divulgación Científica

Artículos, infografías y materiales de comunicación pública de la ciencia desarrollados por nuestro equipo y estudiantes.

{% assign divulgacion_items = site.data.academic.divulgacion %}

{% if divulgacion_items == nil or divulgacion_items.size == 0 %}
  {% assign divulgacion_items = site.data.divulgacion %}
{% endif %}

{% if divulgacion_items == nil or divulgacion_items.size == 0 %}
  {% assign divulgacion_items = site.data.academic.products | where: "type", "divulgacion" %}
{% endif %}

{% if divulgacion_items and divulgacion_items.size > 0 %}
  <section markdown="1" style="margin-top: 2.5rem; margin-bottom: 4rem;">

    {% for item in divulgacion_items %}
      ### {{ item.title }}

      {% if item.authors %}
        **Autores:** {{ item.authors | join: ", " }}
      {% endif %}

      {% if item.journal %}
        **Publicación:** {{ item.journal }}
      {% elsif item.publisher %}
        **Plataforma / Medio:** {{ item.publisher }}
      {% endif %}

      {% if item.year %}
        **Año:** {{ item.year }}
      {% endif %}

      {% if item.description and item.description != "" %}
        {{ item.description }}
      {% endif %}

      {% if item.doi or item.url %}
        {% assign link = item.url %}
        {% if item.doi and item.doi != "" %}
          {% assign link = "https://doi.org/" | append: item.doi %}
        {% endif %}
        [Ver enlace / publicación]({{ link }})
      {% endif %}

      ---
    {% endfor %}

  </section>
{% else %}

  *No hay publicaciones de divulgación registradas actualmente.*

{% endif %}
