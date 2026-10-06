---
layout: default
title: Inicio - JDME
---

# JDME | dariomics

Sitio académico (En desarrollo)

Bienvenido al sitio académico del grupo de investigación **JDME**. Desarrollamos proyectos en neurociencia multisensorial, envejecimiento saludable, análisis de redes de interacciones moleculares y salud pública.

---

## 🎯 Formación Académica e Investigación

Coordinamos actividades para estudiantes interesados en integrarse a proyectos de investigación a través de:

* **Servicio Social** y **Residencia Profesional**
* **Tesis de Licenciatura, Maestría y Doctorado**
* **Voluntariado de Investigación**

👉 Consulta nuestros [[Programas de Servicio Social]](/programas/) disponibles o revisa el perfil de nuestros [[Estudiantes Activos]](/estudiantes/) y [[Egresados]](/egresados/).

---

## 🔬 Programas Activos de Servicio Social

{% assign programs = site.data.service_social.programs | where: "active", true %}

{% if programs.size > 0 %}
{% for program in programs %}
### {{ program.title }}

{% if program.areas %}
**Áreas:** {{ program.areas | join: ", " }}
{% endif %}

{% endfor %}

[Ver detalles y descripción completa de los programas →](/programas/)
{% else %}
*No hay programas de servicio social activos en este momento.*
{% endif %}

---

## 📚 Publicaciones y Productos

Conoce los artículos, libros, preprints y productos de investigación desarrollados por los integrantes del grupo.

👉 [Explorar lista de publicaciones →](/publicaciones/)
