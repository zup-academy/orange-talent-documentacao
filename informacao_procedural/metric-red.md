---
layout: default
title: Métrica tipo RED 
parent: Informação Procedural
---
# Métrica tipo RED

Quando falamos de métricas, existem vários tipos de métricas para responder várias perguntas, como por exemplo:

- Métricas de infraestrutura, como por exemplo: CPU, memória, rede, etc.
- Métricas de negócio, como por exemplo: Quantidade de usuário, compras, vendas, conversão, etc.

E quando falamos de arquitetura distribuída, como por exemplo Microsserviços, existe uma boa prática denominada RED, que tem como objetivo responder três perguntas e deve ser implementada em todos os serviços:

- **R**ate: Quantidade de solicitações, por segundo, que seus serviços estão processando.
- **E**rrors: Quantidade de solicitações com falha por segundo.
- **D**uration: Quantidade de tempo que cada solicitação leva.

Ter essas métricas é extremamente importante e **recomendado** pela Zup, pois ajuda muito em troubleshooting de anomalias em nossos serviços, como por exemplo: 

*“Clientes estão reclamando que está muito lento a Transferência de TED e infelizmente o time de sustentação não consegue encontrar o problema, pois não tem métricas!”*

*“Foi solicitado para o time de desenvolvimento implementar as métricas RED e logo após a sua implementação e implantação em produção, ficou claro o problema!”*

Por conta da mudança no mercado financeiro, a quantidade de solicitações por segundo cresceu muito e os serviços provisionados não conseguem suportar tal carga, ocasionando dois problemas:

Muitas requisições com falha por segundo, ocasionando uma péssima experiência para o usuário \ cliente.

## Dicas 

Felizmente o Spring Boot Actuator, quando configurado o endpoint de métricas, já implementa as métricas do tipo RED, gostaria de saber mais? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/spring-actuator-metrics.md)

- http_server_requests_seconds_count: Quantidade de requisições por segundo
- http_server_requests_seconds_sum: Quantidade de tempo por segundo

Para cálcular a quantidade que cada requisção leva http_server_requests_seconds_sum \ http_server_requests_seconds_count

Para saber quais são sucesso ou erro as mesmas tem a label `status`, conforme exemplo abaixo:

```
http_server_requests_seconds_count{method="POST",outcome="SUCCESS",status="201",uri="/v1/propostas",} 20.0
http_server_requests_seconds_count{method="POST",outcome="CLIENT_ERROR",status="422",uri="/v1/propostas",} 5.0
```
## Informação de Suporte

Gostaria de saber mais sobre Métricas do tipo RED? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/#xref_monitoring_golden-signals)

Está em dúvida sobre o que é Métrica? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/metric.md)
