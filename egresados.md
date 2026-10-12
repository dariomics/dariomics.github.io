---
layout: default
title: Egresados
permalink: /egresados/
---

# Egresados

Personas que han concluido actividades de formación académica.

{% comment %}
  ==============================================================================
  1. CARGA DE DATOS DE LA RED
  ==============================================================================
{% endcomment %}
{% assign people = site.data.people %}
{% assign participations = site.data.academic.participations %}
{% assign programs = site.data.service_social.programs %}
{% assign products = site.data.academic.products %}

{% comment %}
  ==============================================================================
  2. CONTEO DINÁMICO GLOBAL Y POR CATEGORÍA (status == "completed")
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
  {% if participation.status == "completed" %}
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

{% assign total_egresados = count_service_social | plus: count_volunteer | plus: count_residencia | plus: count_thesis_lic | plus: count_thesis_esp | plus: count_thesis_mae | plus: count_thesis_doc %}

{% if total_egresados > 0 %}

**Número total de egresados y ex-colaboradores: {{ total_egresados }}**

{% comment %}
  ==============================================================================
  3. SECCIONES DE RENDERIZADO POR CATEGORÍA
  ==============================================================================
{% endcomment %}

{% comment %} --- SERVICIO SOCIAL --- {% endcomment %}
{% if count_service_social > 0 %}

---

## Servicio Social ({{ count_service_social }})

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "service_social" %}
    {% assign person = people | where: "id", participation.person | first %}
    {% assign program = programs | where: "id", participation.program | first %}

    {% if person and person.public %}
### {{ person.name }}

{% if program %}
**Programa:** {{ program.title }}
{% endif %}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.url and participation.url != "" %}
[Consultar registro / reporte]({{ participation.url }})
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

<br>
    {% endif %}
  {% endif %}
{% endfor %}

{% endif %}

{% comment %} --- VOLUNTARIADO --- {% endcomment %}
{% if count_volunteer > 0 %}

---

## Voluntariado ({{ count_volunteer }})

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "volunteer" %}
    {% assign person = people | where: "id", participation.person | first %}

    {% if person and person.public %}
### {{ person.name }}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.url and participation.url != "" %}
[Consultar registro]({{ participation.url }})
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

<br>
    {% endif %}
  {% endif %}
{% endfor %}

{% endif %}

{% comment %} --- RESIDENCIA PROFESIONAL --- {% endcomment %}
{% if count_residencia > 0 %}

---

## Residencia Profesional ({{ count_residencia }})

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "residencia_profesional" %}
    {% assign person = people | where: "id", participation.person | first %}

    {% if person and person.public %}
### {{ person.name }}

{% if participation.project and participation.project != "" %}
**Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.url and participation.url != "" %}
[Consultar informe / registro]({{ participation.url }})
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

<br>
    {% endif %}
  {% endif %}
{% endfor %}

{% endif %}

{% comment %} --- TESIS DE LICENCIATURA --- {% endcomment %}
{% if count_thesis_lic > 0 %}

---

## Tesis de Licenciatura ({{ count_thesis_lic }})

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "thesis" and participation.level == "licenciatura" %}
    {% assign person = people | where: "id", participation.person | first %}

    {% if person and person.public %}
### {{ person.name }}

**Tesis:** {{ participation.title }}

{% if participation.project and participation.project != "" %}
**Programa / Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.honors and participation.honors != "" %}
**Reconocimiento:** {{ participation.honors }}
{% endif %}

{% if participation.url and participation.url != "" %}
[Consultar tesis]({{ participation.url }})
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

<br>
    {% endif %}
  {% endif %}
{% endfor %}

{% endif %}

{% comment %} --- TRABAJOS DE ESPECIALIDAD --- {% endcomment %}
{% if count_thesis_esp > 0 %}

---

## Trabajos de Especialidad ({{ count_thesis_esp }})

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "thesis" and participation.level == "especialidad" %}
    {% assign person = people | where: "id", participation.person | first %}

    {% if person and person.public %}
### {{ person.name }}

**Trabajo Terminal / Tesis:** {{ participation.title }}

{% if participation.project and participation.project != "" %}
**Programa / Sede:** {{ participation.project }}
{% endif %}

{% if participation.honors and participation.honors != "" %}
**Reconocimiento:** {{ participation.honors }}
{% endif %}

{% if participation.url and participation.url != "" %}
[Consultar trabajo / tesis]({{ participation.url }})
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

<br>
    {% endif %}
  {% endif %}
{% endfor %}

{% endif %}

{% comment %} --- TESIS DE MAESTRÍA --- {% endcomment %}
{% if count_thesis_mae > 0 %}

---

## Tesis de Maestría ({{ count_thesis_mae }})

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "thesis" and participation.level == "maestria" %}
    {% assign person = people | where: "id", participation.person | first %}

    {% if person and person.public %}
### {{ person.name }}

**Tesis:** {{ participation.title }}

{% if participation.project and participation.project != "" %}
**Programa / Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.honors and participation.honors != "" %}
**Reconocimiento:** {{ participation.honors }}
{% endif %}

{% if participation.url and participation.url != "" %}
[Consultar tesis]({{ participation.url }})
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

<br>
    {% endif %}
  {% endif %}
{% endfor %}

{% endif %}

{% comment %} --- TESIS DE DOCTORADO --- {% endcomment %}
{% if count_thesis_doc > 0 %}

---

## Tesis de Doctorado ({{ count_thesis_doc }})

{% for participation in participations %}
  {% if participation.status == "completed" and participation.type == "thesis" and participation.level == "doctorado" %}
    {% assign person = people | where: "id", participation.person | first %}

    {% if person and person.public %}
### {{ person.name }}

**Tesis:** {{ participation.title }}

{% if participation.project and participation.project != "" %}
**Programa / Proyecto:** {{ participation.project }}
{% endif %}

{% if participation.honors and participation.honors != "" %}
**Reconocimiento:** {{ participation.honors }}
{% endif %}

{% if participation.url and participation.url != "" %}
[Consultar tesis]({{ participation.url }})
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

<br>
    {% endif %}
  {% endif %}
{% endfor %}

{% endif %}

{% else %}

No hay egresados ni ex-colaboradores registrados actualmente.

{% endif %}
