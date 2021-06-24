---
layout: default
title: Jaeger - Baggage Item 
parent: Informação Suporte
---
# Jaeger - Baggage Item

Sabemos que no OpenTracing existe o conceito de Span, que é um período que representa uma operação, como por exemplo, 
uma requisição HTTP, na qual contém metadados extremamente importantes, como o **baggage item**, que tem como objetivo 
carregar e propagar informações importantes do Span e dos próximos Spans.

Caso deseje reportar um **baggage item** específico, como por exemplo, email do usuário, precisaremos instrumentar no código!

Vamos fazer isso?

O Spring provê uma classe denominada [Tracer](https://github.com/opentracing/opentracing-java/blob/master/opentracing-api/src/main/java/io/opentracing/Tracer.java) 
na qual você consegue fazer operações relacionadas ao OpenTracing!

1º Precisamos injetar o objeto Tracer, conforme código abaixo:

```java
public class PropostaController {

  private final Tracer tracer;

  public PropostaController(Tracer tracer) {
    this.tracer = tracer;
  }

}
```

2º Agora que temos o objeto, precisamos pegar o `span` ativo, conforme código abaixo:

```java
Span activeSpan = tracer.activeSpan();
```

3º Precisamos definir o **baggage item** desejado, para isso o objetivo Span tem o método `setBaggageItem`, conforme código abaixo:

```java
activeSpan.setBaggageItem("user.email", "luram.archanjo@zup.com.br");
```

Vamos testar?

Para testar precisamos verificar se o Jaeger foi iniciado, conforme está no docker-compose, para isto, vamos abrir em 
nosso navegador favorito o endereço `http://localhost:16686/search`

Agora precisamos iniciar nossa aplicação e fazer algumas operações, como por exemplo, criar uma proposta!

Após fazer várias operações, entre no trace da operação que está o código e verifique se o **baggage item** consta, 
conforme imagem abaixo:

![alt text](/assets/images/open-tracing-008.png "OpenTracing")

No código acima, no segundo serviço a gente obteve o **baggage item** utilizando o método `getBaggageItem()`, 
conforme código abaixo, e sobrescreve o mesmo:

```java
Span activeSpan = tracer.activeSpan();
String userEmail = activeSpan.getBaggageItem("user.email");
activeSpan.setBaggageItem("user.email", userEmail);
```

Agora podemos utilizar vários **baggage itens** para melhorar nosso processo de troubleshooting!

## Dicas 

Use com parcimônia o **baggage item**, pois é um código de infraestrutura (trace) em conjunto com o código de negócio, 
portanto tente segmentar!

## Informações de suporte

Gostaria de saber mais sobre a Jaeger? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://www.jaegertracing.io/docs/1.18/#about)
