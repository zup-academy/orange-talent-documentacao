---
layout: default
title: Como utilizar logs no Spring? 
parent: Informação Suporte
---
# Como utilizar logs no Spring?

Talvez seu código não esteja funcionando e está com dificuldade de encontrar o problema, não se preocupe!

Uma das maneiras de se encontrar um erro é por meio de Logs!

Log de dados é um arquivo de texto gerado por um software para descrever eventos sobre o seu funcionamento, utilização por usuários ou interação com outros sistemas. Um log, após ser gerado, passa a ser incrementado ao longo do tempo com informações que permitem diagnosticar possíveis bugs!

## Vamos fazer isso com Spring!

O [Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-logging) 
utiliza por padrão o [Logback](http://logback.qos.ch/) em caso de utilizar os `Starters`, para utilizar o mesmo, 
precisamos instanciar uma classe denominada Logger, conforme código abaixo:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Exemplo {

    private final Logger logger = LoggerFactory.getLogger(Exemplo.class);

    public void log() {
        logger.info("Log de informação");
        logger.warn("Log de aviso, algo está errado ou faltando! cuidado!");
        logger.error("Log de erro, algo de errado aconteceu!");
        logger.debug("Log de depuração, contém informações mais refinadas, que são mais úteis para depurar um aplicativo");
        logger.trace("Log de rastreabilidade, contém informações mais refinadas do que o DEBUG");
    }

}
```

Pronto!

Agora você pode logar suas informações e diagnosticar possíveis erros mais rápido!

Lembre-se sempre de procurar responder a estratégia dos 5 W's
                    
- **WHO:** Quem está executando a operação.
- **WHAT:** O que indica aquela operação.
- **WHEN:** Quando a operação ocorreu.
- **WHERE:** Onde a operação ocorreu.
- **WHY:** Porquê da linha do log

**Importante**

Você sabia que foi aplicado um dos fatores do The Twelve Factor App?

Você aplicou o fator XI. Logs, na qual diz que devemos tratar logs como fluxos de eventos!

Quer saber mais? Acesse o [link!](../informacao_procedural/twelve-factor-logs.md)

## Dicas

Tenha uma equilíbrio na quantidade de logs da sua aplicação, pois, pouco log complica na depuração de problemas e logs 
demais também!

Trate seus logs como eventos que aconteceram no sistema, como por exemplo:

```java
private final Logger logger = LoggerFactory.getLogger(Exemplo.class);

public void criarProposta(Proposta proposta) {
    // Código omitido
    logger.info("Proposta criada com sucesso!");
}
```

Este log parece não ajudar, pois você não consegue responder qual proposta foi criada, correto!?

Além de tratar seu log como evento, dê informações para ajudar a rastrear o problema, como por exemplo:

```java
private final Logger logger = LoggerFactory.getLogger(Exemplo.class);

public void criarProposta(Proposta proposta) {
    // Código omitido
    logger.info("Proposta documento={} salário={} criada com sucesso!", proposta.getDocumento(), proposta.getSalario());
}
```

**Saída no sistema**

```
11:50:11.558 [main] INFO br.com.zup.PropostaService - Proposta documento=307.896.890-14 salário=-1200 criada com sucesso!
```

Ficou bem mais fácil de identificar, qual proposta, documento, salário e quando a mesma foi criada!

E o mais importante: Sabemos que tem um furo de validação, pois não existe salário negativo!

Eba! Está tudo funcionando! Você sabia que, se logar utilizando o formato JSON o log pode ser indexado e melhora muito o troubleshooting de problemas? Quer saber mais? Acesse o [link!](../informacao_suporte/spring-logging-json.md)

## Informação de Suporte

Quer saber mais sobre logs? acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-logging)

Quer saber mais sobre The Twelve-Factor App? Acesse o [link!](https://12factor.net/pt_br/)
