---
layout: default
title: Inspección de Estructura _data
permalink: /publicaciones/
---

# Diagnóstico de Estructura de Datos

<pre style="background: #f4f4f4; padding: 15px; border-radius: 5px;">
1. Módulos detectados en raíz de _data:
{% for item in site.data %}
   - Key: "{{ item[0] }}" | Tipo: {{ item[1] | inspect | truncate: 60 }}
{% endfor %}

2. Archivos detectados en _data.academic (o variantes):
{% assign academic_node = site.data.academic | default: site.data.Academic | default: site.data.ACADEMIC %}
{% if academic_node %}
  {% for file in academic_node %}
   - Archivo Key: "{{ file[0] }}" | Total elementos: {{ file[1].size | default: file[1].publications.size }}
  {% endfor %}
{% else %}
   - No se encontró ningún nodo 'academic' en site.data.
{% endif %}
</pre>
