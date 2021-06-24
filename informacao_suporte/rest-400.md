---
layout: default
title: Mas porque 400? Entendendo um pouco sobre REST! 
parent: Informação Suporte
---
# Mas porque 400? Entendendo um pouco sobre REST!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define, portanto, toda 
solicitação incorreta devemos representar como **400 Bad Request**, pois o nossa aplicação não consegue processar devido 
algum erro, como por exemplo: campos obrigatórios violados.

Geralmente nos projetos são definidos um padrão de erro para melhorar a identificação do mesmo, conforme exemplo abaixo:

```json
POST http://localhost:8080/v1/cars

HTTP/1.1 400 Bad Request
Content-Type: application/json
{
  "messages": [
    {
      "code": "412.003",
      "description": "Missing or invalid name field."
    },
    {
      "code": "412.004",
      "description": "Missing or invalid address field."
    },
    {
      "code": "412.001",
      "description": "Missing or invalid document field."
    }
  ]
}
```
## Vamos fazer isso com Spring!

O Spring provê uma classe denominada ResponseEntity na qual você consegue passar todas as informações da requisição HTTP, 
como por exemplo, status, body, header, etc.

```java
public ResponseEntity<?> novaProposta(){
    // Código omitido
    return ResponseEntity.status(HttpStatus.BAD_REQUEST.body(body);
}
```

## Informação de Suporte

Quer saber mais sobre status code? Acesse o [link!](../informacao_suporte/rest-status.md)

Quer saber mais sobre REST? Acesse o [link!](https://restfulapi.net/)

Quer saber sobre a especificação? Acesse o [link!](https://tools.ietf.org/html/rfc7231#section-6.5.1)
