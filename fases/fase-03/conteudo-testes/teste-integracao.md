---
layout: default
title: Teste de Integração 
parent: Testes
grand_parent: Fase 03
nav_order: 2
course_name: testes_integracao
---

{% assign course = site.data.fases.fase_03.cursos[page.course_name] %}

{% assign labels = site.data.labels.default_labels %}


# {{  course.title }}

1. [{{ labels.form_start_course }}]({{course.form_start_course}})
2. [{{ labels.alura }}]({{ course.alura }})
3. [{{ labels.form_end_course }}]({{ course.form_end_course }})
4. [{{ labels.form_challenge }}]({{ course.form_challenge }})
