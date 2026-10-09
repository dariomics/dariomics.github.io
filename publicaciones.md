---
layout: default
title: Diagnóstico de Datos
permalink: /publicaciones/
---

# Diagnóstico de Datos de Publicaciones

<pre style="background: #f4f4f4; padding: 15px; border-radius: 5px;">
1. Claves directas en _data: {{ site.data | map: "first" | join: ", " }}
2. Claves en _data.academic: {{ site.data.academic | map: "first" | join: ", " }}
3. Objeto site.data.publicaciones: {{ site.data.publicaciones | inspect }}
4. Objeto site.data.academic.publicaciones: {{ site.data.academic.publicaciones | inspect }}
</pre>
