---
layout: default
title: Programas de Servicio Social
permalink: /programas/
---

# Programas de Servicio Social

Conoce los 4 programas disponibles, sus convocatorias oficiales y los proyectos desarrollados por nuestros estudiantes.

{% assign programs = site.data.service_social.programs %}
{% assign participations = site.data.academic.participations %}
{% assign people = site.data.people %}

<!-- ======================================================================= -->
<!-- 1. ÍNDICE DE TARJETAS DE ACCESO RÁPIDO                                  -->
<!-- ======================================================================= -->
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(270px, 1fr)); gap: 1.25rem; margin: 2rem 0 3.5rem 0;">
{% for program in programs %}
{% if program.active %}
  <div style="background: #f8fafc; border: 1px solid #cbd5e1; border-top: 4px solid #0d253f; border-radius: 8px; padding: 1.25rem; display: flex; flex-direction: column; justify-content: space-between; box-shadow: 0 1px 3px rgba(0,0,0,0.05);">
    <div>
      <h3 style="font-size: 1.05rem; margin: 0 0 0.8rem 0; color: #0d253f; line-height: 1.35;">{{ program.title }}</h3>
      {% if program.areas %}
      <p style="font-size: 0.82rem; color: #64748b; margin-bottom: 1rem; line-height: 1.4;">
        <strong>Áreas:</strong> {{ program.areas | join: " • " }}
      </p>
      {% endif %}
    </div>
    <a href="#{{ program.id }}" style="display: block; text-align: center; background-color: #0d253f; color: #ffffff !important; padding: 0.45rem 0.8rem; border-radius: 6px; font-size: 0.85rem; font-weight: 600; text-decoration: none; margin-top: 0.5rem; transition: background 0.2s;">
      Ver programa y convocatorias ↓
    </a>
  </div>
{% endif %}
{% endfor %}
</div>

<hr style="border: 0; border-top: 1px solid #cbd5e1; margin: 3rem 0;" />

<!-- ======================================================================= -->
<!-- 2. DETALLE DE CADA PROGRAMA                                            -->
<!-- ======================================================================= -->
{% for program in programs %}
{% if program.active %}
<section id="{{ program.id }}" markdown="1" style="margin-top: 3rem; margin-bottom: 4.5rem; padding-bottom: 2.5rem; border-bottom: 2px solid #e0e0e0; scroll-margin-top: 2rem;">

## {{ program.title }}

{% if program.description and program.description != "" %}
{{ program.description }}
{% endif %}

{% if program.sitio_web %}
[🌐 Visitar Sitio Web Oficial del Programa]({{ program.sitio_web }})
{% endif %}

{% if program.areas %}
**Áreas de conocimiento:** {{ program.areas | join: ", " }}
{% endif %}

{% if program.convocatorias %}
### Convocatorias e Instituciones
{% for conv in program.convocatorias %}
* **{{ conv.nombre_institucion }} ({{ conv.institucion }})**
  * **Clave de Registro:** `{% if conv.code %}{{ conv.code }}{% else %}{{ program.code }}{% endif %}`
  * **Instancia:** {{ conv.instancia }}
  * **Ciclo Escolar:** {{ conv.ciclo }}
  {% if conv.link %}[Consultar Ficha Oficial de Registro]({{ conv.link }}){% endif %}
  * **Licenciaturas Convocadas:** {{ conv.licenciaturas | join: ", " }}
{% endfor %}
{% endif %}

<!-- ACORDEÓN DESPLEGABLE CON LA INFORMACIÓN DETALLADA -->
<details style="background: #f8fafc; border: 1px solid #cbd5e1; border-radius: 6px; padding: 0.8rem 1.2rem; margin: 1.5rem 0;">
<summary style="font-weight: 600; color: #0d253f; cursor: pointer; font-size: 0.95rem;">🔍 Ver justificación, metodología, recursos y evaluación del programa</summary>

<div markdown="1" style="margin-top: 1.2rem;">

{% if program.objetivo %}
#### Objetivo
{{ program.objetivo }}
{% endif %}

{% if program.justificacion %}
#### Justificación
{{ program.justificacion }}
{% endif %}

{% if program.desarrollo %}
#### Metodología y Desarrollo
{% for item in program.desarrollo %}
* {{ item }}
{% endfor %}
{% endif %}

{% if program.recursos %}
#### Recursos Disponibles
{% for item in program.recursos %}
* {{ item }}
{% endfor %}
{% endif %}

{% if program.evaluacion %}
#### Criterios de Evaluación
{% for item in program.evaluacion %}
* {{ item }}
{% endfor %}
{% endif %}

{% if program.resultados %}
#### Productos y Resultados Esperados
{% for item in program.resultados %}
* {{ item }}
{% endfor %}
{% endif %}

</div>
</details>

### Estudiantes y Proyectos

{% assign program_participations = participations | where: "program", program.id %}

{% if program_participations.size > 0 %}
{% for participation in program_participations %}{% assign person = people | where: "id", participation.person | first %}{% if person and person.public %}{% assign end_two = participation.end | slice: 0, 2 %}{% assign start_two = participation.start | slice: 0, 2 %}{% if end_two == "20" or end_two == "19" %}{% assign year_label = participation.end | slice: 0, 4 %}{% elsif start_two == "20" or start_two == "19" %}{% assign year_label = participation.start | slice: 0, 4 %}{% else %}{% assign year_label = site.time | date: "%Y" %}{% endif %}* {{ person.name }} ({{ year_label }}).{% if participation.project and participation.project != "" %} **{{ participation.project }}**.{% endif %}
{% endif %}{% endfor %}
{% else %}

*No hay estudiantes registrados en este programa actualmente.*

{% endif %}

<p style="text-align: right; margin-top: 1.5rem;"><a href="#programas-de-servicio-social" style="font-size: 0.85rem; font-weight: 500;">↑ Volver al inicio de programas</a></p>

</section>
{% endif %}
{% endfor %}
