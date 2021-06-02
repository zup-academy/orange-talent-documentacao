---
layout: default
title: Introdução Métricas 
parent: Cursos
grand_parent: Fase 04
nav_order: 6
course_name: introducao_metricas
---

{% assign course = site.data.fases.fase_04.cursos[page.course_name] %}

{% assign labels = site.data.labels.default_labels %}


# {{  course.title }}

1. [{{ labels.form_start_course }}]({{course.form_start_course}})
2. [{{ labels.conteudo }}]({% link informacao_procedural/metric.md %} )
3. [{{ labels.form_end_course }}]({{ course.form_end_course }})
4. [{{ labels.form_challenge }}]({{ course.form_challenge }})
