---
layout: default
title: Kafka
parent: Fase 04
nav_order: 1
grand_parent: Fases
has_children: false
course_name: introducao_kafka
---

{% assign course = site.data.fases.fase_04.cursos[page.course_name] %}

{% assign labels = site.data.labels.default_labels %}


# {{  course.title }}

Com o microservice de propostas implementado, chegou a hora de implementar um novo serviço, o que cuida das transações do cartão de crédito. Como é de praxe, antes de começar, vamos primeiro estudar a teoria necessária. 


1. [{{ labels.form_start_course }}]({{course.form_start_course}})
2. [{{ labels.alura }}]({{ course.alura }})
3. [{{ labels.form_end_course }}]({{ course.form_end_course }})
4. [{{ labels.form_challenge }}]({{ course.form_challenge }})