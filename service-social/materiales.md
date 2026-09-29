---
layout: default
title: Materiales de Servicio Social
permalink: /service-social/materiales/
---

# Materiales de Servicio Social

Materiales de preparación, formación y apoyo para las diferentes etapas del Servicio Social.

{% assign materials = site.data.service_social.materials %}

{% assign has_admission = false %}
{% assign has_induction = false %}
{% assign has_training = false %}
{% assign has_project = false %}
{% assign has_closing = false %}

{% for material in materials %}
  {% if material.stage == "admission" %}
    {% assign has_admission = true %}
  {% elsif material.stage == "induction" %}
    {% assign has_induction = true %}
  {% elsif material.stage == "training" %}
    {% assign has_training = true %}
  {% elsif material.stage == "project" %}
    {% assign has_project = true %}
  {% elsif material.stage == "closing" %}
    {% assign has_closing = true %}
  {% endif %}
{% endfor %}

{% if has_admission %}
## Antes de ingresar

{% for material in materials %}
  {% if material.stage == "admission" %}
### {{ material.title }}

{% if material.description %}
{{ material.description }}
{% endif %}

{% if material.url %}
[Consultar material]({{ material.url }})
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_induction %}
## Inducción

{% for material in materials %}
  {% if material.stage == "induction" %}
### {{ material.title }}

{% if material.description %}
{{ material.description }}
{% endif %}

{% if material.url %}
[Consultar material]({{ material.url }})
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_training %}
## Formación

{% for material in materials %}
  {% if material.stage == "training" %}
### {{ material.title }}

{% if material.description %}
{{ material.description }}
{% endif %}

{% if material.url %}
[Consultar material]({{ material.url }})
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_project %}
## Desarrollo del proyecto

{% for material in materials %}
  {% if material.stage == "project" %}
### {{ material.title }}

{% if material.description %}
{{ material.description }}
{% endif %}

{% if material.url %}
[Consultar material]({{ material.url }})
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}

{% if has_closing %}
## Cierre

{% for material in materials %}
  {% if material.stage == "closing" %}
### {{ material.title }}

{% if material.description %}
{{ material.description }}
{% endif %}

{% if material.url %}
[Consultar material]({{ material.url }})
{% endif %}

---
  {% endif %}
{% endfor %}
{% endif %}
