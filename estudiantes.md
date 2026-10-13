---
layout: default
title: Estudiantes
permalink: /estudiantes/
---

# Estudiantes

Personas que actualmente participan en actividades de formación académica.

{% comment %}
  ==============================================================================
  1. CARGA DE DATOS DE LA RED
  ==============================================================================
{% endcomment %}
{% assign people = site.data.people %}
{% assign participations = site.data.academic.participations %}
{% assign programs = site.data.service_social.programs %}
{% assign taxonomia = site.data.taxonomia %}
{% assign pubs_data = site.data.academic.publicaciones.publications | default: site.data.academic.publicaciones %}
{% assign divs_data = site.data.academic.divulgacion.divulgacion | default: site.data.academic.divulgacion %}

{% comment %}
  ==============================================================================
  2. CONTEO DINÁMICO GLOBAL Y POR CATEGORÍA (status == "active")
  ==============================================================================
{% endcomment %}
{% assign count_service_social = 0 %}
{% assign count_volunteer = 0 %}
{% assign count_residencia = 0 %}
{% assign count_thesis_lic = 0 %}
{% assign count_thesis_esp = 0 %}
{% assign count_thesis_mae = 0 %}
{% assign count_thesis_doc = 0 %}

{% for participation in participations %}
  {% if participation.status == "active" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% if person and person.public %}
      {% if participation.type == "service_social" %}
        {% assign count_service_social = count_service_social | plus: 1 %}
      {% elsif participation.type == "volunteer" %}
        {% assign count_volunteer = count_volunteer | plus: 1 %}
      {% elsif participation.type == "residencia_profesional" %}
        {% assign count_residencia = count_residencia | plus: 1 %}
      {% elsif participation.type == "thesis" %}
        {% if participation.level == "licenciatura" %}
          {% assign count_thesis_lic = count_thesis_lic | plus: 1 %}
        {% elsif participation.level == "especialidad" %}
          {% assign count_thesis_esp = count_thesis_esp | plus: 1 %}
        {% elsif participation.level == "maestria" %}
          {% assign count_thesis_mae = count_thesis_mae | plus: 1 %}
        {% elsif participation.level == "doctorado" %}
          {% assign count_thesis_doc = count_thesis_doc | plus: 1 %}
        {% endif %}
      {% endif %}
    {% endif %}
  {% endif %}
{% endfor %}

{% assign total_active = count_service_social | plus: count_volunteer | plus: count_residencia | plus: count_thesis_lic | plus: count_thesis_esp | plus: count_thesis_mae | plus: count_thesis_doc %}

{% if total_active > 0 %}

**Número total de alumnos y colaboradores activos: {{ total_active }}**

{% comment %}
  ==============================================================================
  3. SERVICIO SOCIAL
  ==============================================================================
{% endcomment %}
{% if count_service_social > 0 %}

---

## Servicio Social ({{ count_service_social }})

{% for participation in participations %}
  {% if participation.status == "active" and participation.type == "service_social" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% assign procedencia = "" %}
{% if participation.degree_program and participation.degree_program != "" %}
  {% assign procedencia = participation.degree_program %}
{% endif %}
{% if participation.institution and participation.institution != "" %}
  {% if procedencia != "" %}
    {% assign procedencia = procedencia | append: ", " | append: participation.institution %}
  {% else %}
    {% assign procedencia = participation.institution %}
  {% endif %}
{% endif %}
{% if procedencia == "" and person.institution %}
  {% assign procedencia = person.institution %}
{% endif %}
{% if procedencia != "" %}
**Procedencia:** {{ procedencia }}
{% endif %}

{% assign prog_title = program.title | default: participation.program %}
{% if prog_title and prog_title != "" %}
**Programa:** {{ prog_title }}
{% endif %}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**
{% for product_id in participation.products %}
  {% assign match_pub = pubs_data | where: "id", product_id | first %}
  {% assign match_div = divs_data | where: "id", product_id | first %}
  {% assign product = match_pub | default: match_div %}

  {% if product %}
    {% assign label = "" %}
    {% for cat in taxonomia %}
      {% assign items = cat[1] %}
      {% for item in items %}
        {% if item.type == product.type %}
          {% assign label = item.label | default: item.singular %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    {% if label == "" or label == nil %}
      {% assign label = product.type | replace: "_", " " | capitalize %}
    {% endif %}
- **{{ label }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% comment %}
  ==============================================================================
  4. VOLUNTARIADO
  ==============================================================================
{% endcomment %}
{% if count_volunteer > 0 %}

---

## Voluntariado ({{ count_volunteer }})

{% for participation in participations %}
  {% if participation.status == "active" and participation.type == "volunteer" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% assign procedencia = "" %}
{% if participation.degree_program and participation.degree_program != "" %}
  {% assign procedencia = participation.degree_program %}
{% endif %}
{% if participation.institution and participation.institution != "" %}
  {% if procedencia != "" %}
    {% assign procedencia = procedencia | append: ", " | append: participation.institution %}
  {% else %}
    {% assign procedencia = participation.institution %}
  {% endif %}
{% endif %}
{% if procedencia == "" and person.institution %}
  {% assign procedencia = person.institution %}
{% endif %}
{% if procedencia != "" %}
**Procedencia:** {{ procedencia }}
{% endif %}

{% assign prog_title = program.title | default: participation.program %}
{% if prog_title and prog_title != "" %}
**Programa:** {{ prog_title }}
{% endif %}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**
{% for product_id in participation.products %}
  {% assign match_pub = pubs_data | where: "id", product_id | first %}
  {% assign match_div = divs_data | where: "id", product_id | first %}
  {% assign product = match_pub | default: match_div %}

  {% if product %}
    {% assign label = "" %}
    {% for cat in taxonomia %}
      {% assign items = cat[1] %}
      {% for item in items %}
        {% if item.type == product.type %}
          {% assign label = item.label | default: item.singular %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    {% if label == "" or label == nil %}
      {% assign label = product.type | replace: "_", " " | capitalize %}
    {% endif %}
- **{{ label }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% comment %}
  ==============================================================================
  5. RESIDENCIA PROFESIONAL
  ==============================================================================
{% endcomment %}
{% if count_residencia > 0 %}

---

## Residencia Profesional ({{ count_residencia }})

{% for participation in participations %}
  {% if participation.status == "active" and participation.type == "residencia_profesional" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% assign procedencia = "" %}
{% if participation.degree_program and participation.degree_program != "" %}
  {% assign procedencia = participation.degree_program %}
{% endif %}
{% if participation.institution and participation.institution != "" %}
  {% if procedencia != "" %}
    {% assign procedencia = procedencia | append: ", " | append: participation.institution %}
  {% else %}
    {% assign procedencia = participation.institution %}
  {% endif %}
{% endif %}
{% if procedencia == "" and person.institution %}
  {% assign procedencia = person.institution %}
{% endif %}
{% if procedencia != "" %}
**Procedencia:** {{ procedencia }}
{% endif %}

{% assign prog_title = program.title | default: participation.program %}
{% if prog_title and prog_title != "" %}
**Programa:** {{ prog_title }}
{% endif %}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**
{% for product_id in participation.products %}
  {% assign match_pub = pubs_data | where: "id", product_id | first %}
  {% assign match_div = divs_data | where: "id", product_id | first %}
  {% assign product = match_pub | default: match_div %}

  {% if product %}
    {% assign label = "" %}
    {% for cat in taxonomia %}
      {% assign items = cat[1] %}
      {% for item in items %}
        {% if item.type == product.type %}
          {% assign label = item.label | default: item.singular %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    {% if label == "" or label == nil %}
      {% assign label = product.type | replace: "_", " " | capitalize %}
    {% endif %}
- **{{ label }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% comment %}
  ==============================================================================
  6. TESIS DE LICENCIATURA
  ==============================================================================
{% endcomment %}
{% if count_thesis_lic > 0 %}

---

## Tesis de Licenciatura ({{ count_thesis_lic }})

{% for participation in participations %}
  {% if participation.status == "active" and participation.type == "thesis" and participation.level == "licenciatura" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% assign procedencia = "" %}
{% if participation.degree_program and participation.degree_program != "" %}
  {% assign procedencia = participation.degree_program %}
{% endif %}
{% if participation.institution and participation.institution != "" %}
  {% if procedencia != "" %}
    {% assign procedencia = procedencia | append: ", " | append: participation.institution %}
  {% else %}
    {% assign procedencia = participation.institution %}
  {% endif %}
{% endif %}
{% if procedencia == "" and person.institution %}
  {% assign procedencia = person.institution %}
{% endif %}
{% if procedencia != "" %}
**Procedencia:** {{ procedencia }}
{% endif %}

{% assign prog_title = program.title | default: participation.program %}
{% if prog_title and prog_title != "" %}
**Programa:** {{ prog_title }}
{% endif %}

{% if participation.title and participation.title != "" %}
**Tesis:** {{ participation.title }}
{% endif %}
{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**
{% for product_id in participation.products %}
  {% assign match_pub = pubs_data | where: "id", product_id | first %}
  {% assign match_div = divs_data | where: "id", product_id | first %}
  {% assign product = match_pub | default: match_div %}

  {% if product %}
    {% assign label = "" %}
    {% for cat in taxonomia %}
      {% assign items = cat[1] %}
      {% for item in items %}
        {% if item.type == product.type %}
          {% assign label = item.label | default: item.singular %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    {% if label == "" or label == nil %}
      {% assign label = product.type | replace: "_", " " | capitalize %}
    {% endif %}
- **{{ label }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% comment %}
  ==============================================================================
  7. TRABAJOS DE ESPECIALIDAD
  ==============================================================================
{% endcomment %}
{% if count_thesis_esp > 0 %}

---

## Trabajos de Especialidad ({{ count_thesis_esp }})

{% for participation in participations %}
  {% if participation.status == "active" and participation.type == "thesis" and participation.level == "especialidad" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% assign procedencia = "" %}
{% if participation.degree_program and participation.degree_program != "" %}
  {% assign procedencia = participation.degree_program %}
{% endif %}
{% if participation.institution and participation.institution != "" %}
  {% if procedencia != "" %}
    {% assign procedencia = procedencia | append: ", " | append: participation.institution %}
  {% else %}
    {% assign procedencia = participation.institution %}
  {% endif %}
{% endif %}
{% if procedencia == "" and person.institution %}
  {% assign procedencia = person.institution %}
{% endif %}
{% if procedencia != "" %}
**Procedencia:** {{ procedencia }}
{% endif %}

{% assign prog_title = program.title | default: participation.program %}
{% if prog_title and prog_title != "" %}
**Programa:** {{ prog_title }}
{% endif %}

{% if participation.title and participation.title != "" %}
**Trabajo Terminal / Tesis:** {{ participation.title }}
{% endif %}
{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**
{% for product_id in participation.products %}
  {% assign match_pub = pubs_data | where: "id", product_id | first %}
  {% assign match_div = divs_data | where: "id", product_id | first %}
  {% assign product = match_pub | default: match_div %}

  {% if product %}
    {% assign label = "" %}
    {% for cat in taxonomia %}
      {% assign items = cat[1] %}
      {% for item in items %}
        {% if item.type == product.type %}
          {% assign label = item.label | default: item.singular %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    {% if label == "" or label == nil %}
      {% assign label = product.type | replace: "_", " " | capitalize %}
    {% endif %}
- **{{ label }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% comment %}
  ==============================================================================
  8. TESIS DE MAESTRÍA
  ==============================================================================
{% endcomment %}
{% if count_thesis_mae > 0 %}

---

## Tesis de Maestría ({{ count_thesis_mae }})

{% for participation in participations %}
  {% if participation.status == "active" and participation.type == "thesis" and participation.level == "maestria" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% assign procedencia = "" %}
{% if participation.degree_program and participation.degree_program != "" %}
  {% assign procedencia = participation.degree_program %}
{% endif %}
{% if participation.institution and participation.institution != "" %}
  {% if procedencia != "" %}
    {% assign procedencia = procedencia | append: ", " | append: participation.institution %}
  {% else %}
    {% assign procedencia = participation.institution %}
  {% endif %}
{% endif %}
{% if procedencia == "" and person.institution %}
  {% assign procedencia = person.institution %}
{% endif %}
{% if procedencia != "" %}
**Procedencia:** {{ procedencia }}
{% endif %}

{% assign prog_title = program.title | default: participation.program %}
{% if prog_title and prog_title != "" %}
**Programa:** {{ prog_title }}
{% endif %}

{% if participation.title and participation.title != "" %}
**Tesis:** {{ participation.title }}
{% endif %}
{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**
{% for product_id in participation.products %}
  {% assign match_pub = pubs_data | where: "id", product_id | first %}
  {% assign match_div = divs_data | where: "id", product_id | first %}
  {% assign product = match_pub | default: match_div %}

  {% if product %}
    {% assign label = "" %}
    {% for cat in taxonomia %}
      {% assign items = cat[1] %}
      {% for item in items %}
        {% if item.type == product.type %}
          {% assign label = item.label | default: item.singular %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    {% if label == "" or label == nil %}
      {% assign label = product.type | replace: "_", " " | capitalize %}
    {% endif %}
- **{{ label }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% comment %}
  ==============================================================================
  9. TESIS DE DOCTORADO
  ==============================================================================
{% endcomment %}
{% if count_thesis_doc > 0 %}

---

## Tesis de Doctorado ({{ count_thesis_doc }})

{% for participation in participations %}
  {% if participation.status == "active" and participation.type == "thesis" and participation.level == "doctorado" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% assign procedencia = "" %}
{% if participation.degree_program and participation.degree_program != "" %}
  {% assign procedencia = participation.degree_program %}
{% endif %}
{% if participation.institution and participation.institution != "" %}
  {% if procedencia != "" %}
    {% assign procedencia = procedencia | append: ", " | append: participation.institution %}
  {% else %}
    {% assign procedencia = participation.institution %}
  {% endif %}
{% endif %}
{% if procedencia == "" and person.institution %}
  {% assign procedencia = person.institution %}
{% endif %}
{% if procedencia != "" %}
**Procedencia:** {{ procedencia }}
{% endif %}

{% assign prog_title = program.title | default: participation.program %}
{% if prog_title and prog_title != "" %}
**Programa:** {{ prog_title }}
{% endif %}

{% if participation.title and participation.title != "" %}
**Tesis:** {{ participation.title }}
{% endif %}
{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**
{% for product_id in participation.products %}
  {% assign match_pub = pubs_data | where: "id", product_id | first %}
  {% assign match_div = divs_data | where: "id", product_id | first %}
  {% assign product = match_pub | default: match_div %}

  {% if product %}
    {% assign label = "" %}
    {% for cat in taxonomia %}
      {% assign items = cat[1] %}
      {% for item in items %}
        {% if item.type == product.type %}
          {% assign label = item.label | default: item.singular %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    {% if label == "" or label == nil %}
      {% assign label = product.type | replace: "_", " " | capitalize %}
    {% endif %}
- **{{ label }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% else %}

No hay estudiantes ni colaboradores activos registrados actualmente.

{% endif %}
