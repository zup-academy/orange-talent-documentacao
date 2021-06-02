---
layout: default
title: Healthcheck 
parent: Cursos
grand_parent: Fase 04
nav_order: 2
course_name: healthcheck
---

{% assign course = site.data.fases.fase_04.cursos[page.course_name] %}

{% assign labels = site.data.labels.default_labels %}


# {{  course.title }}

1. [{{ labels.form_start_course }}]({{course.form_start_course}})
2. [{{ labels.conteudo }}]({% link informacao_procedural/health_check_readiness_check_&_spring_boot_actuator.md %} )
3. [{{ labels.form_end_course }}]({{ course.form_end_course }})
4. [{{ labels.form_challenge }}]({{ course.form_challenge }})
