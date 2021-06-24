---
layout: default
title: Configurando nossa fonte de dados no Grafana! 
parent: Informação Procedural
---
# Configurando nossa fonte de dados no Grafana!

O Grafana é uma ferramenta para criação e visualização de gŕaficos, ele não
gerencia nenhum tipo de dados relacionado a métricas. Esses dados devem
ser consultados em alguma fonte de dados, o grafana dá suporte há uma
série de ferramentas que possuem dados dos mais diversos tipos.

Podemos configurar como fonte de dados uma fonte de ElasticSearch onde temos dados
de aplicações, ou também podemos consultar dados de um Jaeger que são relacionados à
Trace Distribuído. Mas para nosso caso de uso vamos utilizar o Prometheus como fonte de
dados, no nosso Prometheus constam todos métricas que reportamos através de nossas aplicações.

Então vamos ao menu de configuração de Data Sources, menu localizado no canto superior esquerdo.

Se você não encontrou, sem problemas a imagem abaixo pode te ajudar!!!

![comecando configurar datastore](/assets/images/comecar_configurar_datastore_grafana.png " comecando configurar datastore")

Nesta tela temos um botão azul, em que podemos iniciar o procedimento de configurar nosso Datasource, então
não vamos perder tempo e ir clicar ele!

Depois desse passo você será apresentado à próxima tela onde devemos escolher o tipo de
Datasource que queremos configurar, no nosso caso vamos escolher configurar um Prometheus, então clique nele!

Vamos dar uma olhadinha nesta tela:

![ds prometheus](/assets/images/escolhendo_tipo_ds_grafana.png " ds prometheus")

Estamos indo bem!

No nosso próximo passo precisamos inserir configurações relacionadas ao 
**Prometheus**, como por exemplo localização dele na rede, modelos de autenticação, tempos de scrape e mais algumas
configurações que dependendo do seu caso de uso possa fazer sentido.

Para nosso propósito, não incluímos nenhum modelo de segurança afinal estamos
rodando em ambiente de desenvolvimento local.

**Nota importante**

Lembre-se, todos os outros ambientes devem possuir no mínimo autenticação por senha, e proteção via rede, nunca exponha 
suas métricas de maneira pública, elas podem conter informações relevantes para o negócio, bem como informações preciosas 
para possíveis ataques.

Então vamos configurar nosso **Prometheus**!

Como podemos observar na tela abaixo colocamos o endereço **http://localhost:9090** na configuração, mas porque este endereço?

![config prometheus](/assets/images/endereco_prometheus.png " config prometheus")

Depois de inserir as informações podemos testar nossas configurações, então clique em **Save & Test**. Se tudo ocorreu
bem você deve ter recebido a seguinte mensagem "Datasource is working", isso indica sucesso!

**Grafana** e **Prometheus** conectados agora podemos criar nossos próprios gráfico _"bacanudos"_, vamos explorar algumas 
funcionalidades do grafana, agora você tem duas opções:

* Criar um gráfico manualmente
* Importar um pré-configurado que consegue ler configurações padrão de aplicações Spring Boot. [Aqui tem uma detalhamento completo
de como você pode fazer isso!](importando_graficos_grafana.md)

## Informações de suporte

* Se você não tem idéia do que é o Grafana! Não se preocupe! [Aqui você pode encontrar uma boa definição!](https://grafana.com/) 