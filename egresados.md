---
layout: default
title: Egresados
permalink: /egresados/
---

# Egresados

Personas que han concluido actividades de formación académica.

{% assign people = site.data.people %}
{% assign participations = site.data.academic.participations %}
{% assign programs = site.data.service_social.programs %}
{% assign products = site.data.academic.products %}

{% assign has_service_social = false %}
{% assign has_volunteers = false %}
{% assign has_residencia_profesional = false %}
{% assign has_thesis_lic = false %}
{% assign has_thesis_maestria = false %}
{% assign has_thesis_doctorado = false %}

{% for participation in participations %}
  {% if participation.status == "completed" %}
    {% if participation.type == "service_social" %}
      {% assign has_service_social = true %}
    {% elsif participation.type == "volunteer" %}
      {% assign has_volunteers = true %}
    {% elsif participation.type == "residencia_profesional" %}
      {% assign has_residencia_profesional = true %}
    {% elsif participation.type == "thesis" %}
      {% if participation.level == "licenciatura" %}
        {% assign has_thesis_lic = true %}
      {% elsif participation.level == "maestria" %}
        {% assign has_thesis_maestria = true %}
      {% elsif participation.level == "doctorado" %}
        {% assign has_thesis_doctorado = true %}
      {% endif %}
    {% endif %}
  {% endif %}
{% endfor %}

{% if has_service_social %}
## Servicio Social

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "service_social" %}

    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person.public %}
### {{ person.name }}

{% if program %}
**Programa:** {{ program.title }}
{% endif %}

**Periodo:** {{ participation.start }} – {{ participation.end }}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**

{% for product_id in participation.products %}
  {% assign product = products | where: "id", product_id | first %}
  {% if product %}
- **{{ product.type }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

---
    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% if has_volunteers %}
## Voluntariado

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "volunteer" %}

    {% assign person = people | where: "id", participation.person | first %}

    {% if person.public %}
### {{ person.name }}

**Periodo:** {{ participation.start }} – {{ participation.end }}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**

{% for product_id in participation.products %}
  {% assign product = products | where: "id", product_id | first %}
  {% if product %}
- **{{ product.type }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

---
    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% if has_residencia_profesional %}
## Residencia Profesional

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "residencia_profesional" %}

    {% assign person = people | where: "id", participation.person | first %}

    {% if person.public %}
### {{ person.name }}

**Periodo:** {{ participation.start }} – {{ participation.end }}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**

{% for product_id in participation.products %}
  {% assign product = products | where: "id", product_id | first %}
  {% if product %}
- **{{ product.type }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

---
    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% if has_thesis_lic %}
## Tesis de Licenciatura

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "thesis" and participation.level == "licenciatura" %}

    {% assign person = people | where: "id", participation.person | first %}

    {% if person.public %}
### {{ person.name }}

**Tesis:** {{ participation.title }}

**Periodo:** {{ participation.start }} – {{ participation.end }}

{% if participation.project and participation.project != "" %}
**Programa / Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**

{% for product_id in participation.products %}
  {% assign product = products | where: "id", product_id | first %}
  {% if product %}
- **{{ product.type }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

---
    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% if has_thesis_maestria %}
## Tesis de Maestría

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "thesis" and participation.level == "maestria" %}

    {% assign person = people | where: "id", participation.person | first %}

    {% if person.public %}
### {{ person.name }}

**Tesis:** {{ participation.title }}

**Periodo:** {{ participation.start }} – {{ participation.end }}

{% if participation.project and participation.project != "" %}
**Programa / Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**

{% for product_id in participation.products %}
  {% assign product = products | where: "id", product_id | first %}
  {% if product %}
- **{{ product.type }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

---
    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}

{% if has_thesis_doctorado %}
## Tesis de Doctorado

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "thesis" and participation.level == "doctorado" %}

    {% assign person = people | where: "id", participation.person | first %}

    {% if person.public %}
### {{ person.name }}

**Tesis:** {{ participation.title }}

**Periodo:** {{ participation.start }} – {{ participation.end }}

{% if participation.project and participation.project != "" %}
**Programa / Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.products and participation.products.size > 0 %}
**Productos:**

{% for product_id in participation.products %}
  {% assign product = products | where: "id", product_id | first %}
  {% if product %}
- **{{ product.type }}:** {{ product.title }}
  {% endif %}
{% endfor %}
{% endif %}

---
    {% endif %}
  {% endif %}
{% endfor %}
{% endif %}
