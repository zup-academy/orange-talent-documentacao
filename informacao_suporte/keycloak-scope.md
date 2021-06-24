---
layout: default
title: Criando escopos no Keycloak 
parent: Informação Suporte
---
# Criando escopos no Keycloak

Como já vimos anteriormente o Keycloak é uma ferramenta que permite que possamos gerenciar nossas aplicações (clientes),
desta maneira garantimos essas aplicações, como browser, aplicativos e serviços estejam configuradas e seguras. 

Essas aplicações podem ter inúmeros escopos, que são utilizados para permitir, habilitar, bloquear determinadas ações no 
sistema, como por exemplo: Somente quem tem o escopo ADMIN pode ver X,Y,Z página.

Vamos criar nosso primeiro escopo e associar a um cliente?

> Está em dúvida sobre o que é um Cliente e como criar? Não se preocupe! [Escrevemos esse material para você!](keycloak-client.md)

Se você usou nosso [docker-compose.yaml](../ops/docker-compose.yaml) você poderá verificar
que temos um elemento chamado **keycloak**. Abaixo segue o fragmento

```yaml
  keycloak:
    image: jboss/keycloak
    ports:
      - 18443:8443
      - 18080:8080
      - 19990:9990
    depends_on:
    ##
    ## restante omitido
    ##
    environment:
    ##
    ## restante omitido
    ##
``` 
A porta de administração padrão do keycloak é **8080**, mas perceba: fizemos um "bind" para
porta **18080**.

Faça o login na plataforma, caso você tenha algum problema em realizar o login [este link pode te ajudar](keycloak-login.md)

Depois disso você deve certificar-se que você esteja no seu Realm previamente criado. Se por algum motivo você não criou seu Realm, sem problemas
[este link vai te ajudar com isso](keycloak-realm.md)

No canto superior esquerdo você pode ver o Realm selecionado, na figura abaixo estamos no _"Nosso-cartão"_, no menu **Configure** 
seleciona a opção **Client Scopes** e então clique no botão **Create**. Como na figura abaixo:

![image](/assets/images/keycloak/keycloak-scope-001.jpg "Image")

Depois você será redirecionado para uma página onde você deverá preencher informações do escopo, como na figura abaixo

![image](/assets/images/keycloak/keycloak-scope-002.jpg "Image")

Você criou seu primeiro cliente! Vamos associar em nossa aplicação?

Para associar o escopo criado em nossa aplicação, no menu **Configure**  seleciona a opção **Clients** e então clique 
no botão **Edit** do cliente desejado. Como na figura abaixo:

![image](/assets/images/keycloak/keycloak-scope-003.jpg "Image")

Depois você será redirecionado para a página de modificação do seu cliente, clique na aba **Client Scopes**, nela terá 
duas opções **Default Client Scopes** que são os escopos padrões que a aplicação irá ter e **Optional Client Scopes** que 
são os escopos opcionais que sua aplicação poderá prover!

Encontre e selecione o escopo criado na seção **Default Client Scopes** e clique em **Add selected**, conforme imagem 
abaixo:

![image](/assets/images/keycloak/keycloak-scope-004.jpg "Image")

Eba! Está tudo configurado! Para testar gera uma novo token e verifica se o escopo criado está contido no mesmo, conforme 
exemplo abaixo:

**Requisição**

```shell script
curl --location --request POST 'http://localhost:18080/auth/realms/nosso-cartao/protocol/openid-connect/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username=luramarchanjo' \
--data-urlencode 'password=3`!!z[MVGxuJB2>Y' \
--data-urlencode 'client_id=nosso-cartao-client' \
--data-urlencode 'client_secret=1610ed88-3a65-45ab-950a-c856f9ee17d2' \
--data-urlencode 'scope=proposal:read proposal:write'
```

**Token**

```json
{
    "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJMV2Zic1hycUJINHBTM2JVTWN4TzRaRnpxYjBFRnBrdjZ5RXhUY2NMb1pnIn0.eyJleHAiOjE2MDA0NDAyMjcsImlhdCI6MTYwMDQzOTkyNywianRpIjoiZjAzZGM4YmQtZmI4Zi00NDQ5LWIyZGQtZWYwZThmODhmNWQ1IiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDoxODA4MC9hdXRoL3JlYWxtcy9ub3Nzby1jYXJ0YW8iLCJhdWQiOiJhY2NvdW50Iiwic3ViIjoiNTFmNGQzY2YtZGU4Yi00NDllLWFmZWUtNDdiNTQ1MzU0NmU1IiwidHlwIjoiQmVhcmVyIiwiYXpwIjoibm9zc28tY2FydGFvLWNsaWVudCIsInNlc3Npb25fc3RhdGUiOiIzNWE5ZDUwOS0xMzkzLTQyY2ItYjc2Ny05ZmFmYmU1NmU3NjYiLCJhY3IiOiIxIiwicmVhbG1fYWNjZXNzIjp7InJvbGVzIjpbIm9mZmxpbmVfYWNjZXNzIiwidW1hX2F1dGhvcml6YXRpb24iXX0sInJlc291cmNlX2FjY2VzcyI6eyJhY2NvdW50Ijp7InJvbGVzIjpbIm1hbmFnZS1hY2NvdW50IiwibWFuYWdlLWFjY291bnQtbGlua3MiLCJ2aWV3LXByb2ZpbGUiXX19LCJzY29wZSI6Im1ldS1wcmltZWlyby1lc2NvcG8gcHJvZmlsZSBlbWFpbCIsImNsaWVudElkIjoibm9zc28tY2FydGFvLWNsaWVudCIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwiY2xpZW50SG9zdCI6IjE3Mi4xNy4wLjEiLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJzZXJ2aWNlLWFjY291bnQtbm9zc28tY2FydGFvLWNsaWVudCIsImNsaWVudEFkZHJlc3MiOiIxNzIuMTcuMC4xIn0.Gkqumkq5N_mH1L40695yzPk0b9Zbu-GdjUh5LtZudtAb6LSgPjLNTU5thQYgGdq6PvEfWaSpCDi75ewbkb5SlNLOMlXa4NlrSjBjLMBowStugKDm7UaYLUcf4Cjf-I5_Vx5AmsSQuhT2LfaefUe6x0RKJPEruGQdeZGXqW7F0i-gbhXSYxB5MKFeX_6rZBfmE9Ch3j4TlkCvze7EITc-Q-roLaDtFI654SHvOLv7bpf07kec0REzsMs7oAwpJ3i4VzPhsXKK52EQUpwdBrrd0p4pk9JeM1l0lIc13c1N64-y7BlgKqkynWWJMEPC8nOqNNDLUbP5EaQWq4d4kw9hng",
    "expires_in": 300,
    "refresh_expires_in": 1800,
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI2Mjg0OTFhOC0xNTRiLTQ2MDItYWJmYi0wYThhNWE1Njk0ZDgifQ.eyJleHAiOjE2MDA0NDE3MjcsImlhdCI6MTYwMDQzOTkyNywianRpIjoiOGNhMmU5MjMtYjJiYi00MDBiLWJkNTUtODAzNDkyNmI4YTlmIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDoxODA4MC9hdXRoL3JlYWxtcy9ub3Nzby1jYXJ0YW8iLCJhdWQiOiJodHRwOi8vbG9jYWxob3N0OjE4MDgwL2F1dGgvcmVhbG1zL25vc3NvLWNhcnRhbyIsInN1YiI6IjUxZjRkM2NmLWRlOGItNDQ5ZS1hZmVlLTQ3YjU0NTM1NDZlNSIsInR5cCI6IlJlZnJlc2giLCJhenAiOiJub3Nzby1jYXJ0YW8tY2xpZW50Iiwic2Vzc2lvbl9zdGF0ZSI6IjM1YTlkNTA5LTEzOTMtNDJjYi1iNzY3LTlmYWZiZTU2ZTc2NiIsInNjb3BlIjoibWV1LXByaW1laXJvLWVzY29wbyBwcm9maWxlIGVtYWlsIn0.ZkZXg2QFF6APBqzn4G7F1D99f1MU9wZdeu_zcebDHhE",
    "token_type": "bearer",
    "not-before-policy": 0,
    "session_state": "35a9d509-1393-42cb-b767-9fafbe56e766",
    "scope": "meu-primeiro-escopo profile email"
}
```
Agora que você gerou o token é preciso fornecer o mesmo nas APIs que requerem autenticação!

Para passar o token nas APIs que requerem autenticação é preciso enviar o **Header** denominado **Authorization** com o 
o valor do **access_token** com o prefixo **Bearer**!

Ficou confuso? Não tem problema, segue exemplo!

```shell script
curl --location --request POST 'http://localhost:8080/v1/proposals' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJpWmlVcUJPSC1qU1hKNkJOODVldWxISWdWeDJKeWVRUmJncXY4eDlYYzRvIn0.eyJleHAiOjE2MDQ0MzI4NTcsImlhdCI6MTYwNDQzMjU1NywianRpIjoiYzBkM2JlOTUtNmViZC00NTQzLTk1OWMtYjA0Mjg0MjU0ZDAxIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDoxODA4MC9hdXRoL3JlYWxtcy9ub3Nzby1jYXJ0YW8iLCJzdWIiOiJlY2U0ZDZjZi0yNGMxLTRiMmQtYjQ5MS03ODVmOGZhMzY4NzUiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJub3Nzby1jYXJ0YW8tY2xpZW50Iiwic2Vzc2lvbl9zdGF0ZSI6IjZlMmI5YjI0LWM0ZDQtNGU5YS04YzMyLWRkNzk2ZGE0N2Q0MyIsImFjciI6IjEiLCJzY29wZSI6InRyYW5zYWN0aW9uOnJlYWQgaW52b2ljZTp3cml0ZSBpbnZvaWNlOnJlYWQgdHJhbnNhY3Rpb246d3JpdGUgcHJvZmlsZSBwcm9wb3NhbDp3cml0ZSBwcm9wb3NhbDpyZWFkIGVtYWlsIiwiZW1haWxfdmVyaWZpZWQiOmZhbHNlLCJuYW1lIjoiTHVyYW0gQXJjaGFuam8iLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJsdXJhbWFyY2hhbmpvIiwiZ2l2ZW5fbmFtZSI6Ikx1cmFtIiwiZmFtaWx5X25hbWUiOiJBcmNoYW5qbyIsImVtYWlsIjoibHVyYW0uYXJjaGFuam9AenVwLmNvbS5iciJ9.MRGQ86OJVDiLJBq1h6qeS4M68SNV7zH0mIMaBk1Ip9MjlfAaHS5S-DSAcjy4Rp-0E-Ea8lAkOA0O_ldx0ScxiSWyxf80LSjNmCWrNWhI4PYbdxAg_WwMusXlLJtdlT4aeWXdmcaIQivz-8qKacTPhLqzu_M8FPPEYmUpt2WmI2nqdGkwWxzpKhEa7D2Sid_qFIDjgTy1OTj0_6TMpOnpNzmWOsBfKJpDPdxebi-cN2ZrkPVO7gLeLhG0rIGCJSzr3PoZfI9X7hi39WpYKsuIQOx8U7NuIknn0FOvn3OwaUdkC4t5nV3bswS70GocSX86P2Eun2DxMOBmpC-BW5Fgkg' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name" : "Veronica Mueller",
    "document" : "27268257708",
    "email": "luram.archanjo@zup.com.br",
    "salary" : 840.15,
    "address" : {
        "state" : "São Paulo",
        "city" : "Schambergerchester",
        "street" : "McDermott Field, 202"
    }
}'
```

## Informações de suporte

* Talvez você possa estar se perguntando, qual a função sobre o docker-compose. [Aqui você pode encontrar](https://docs.docker.com/compose/)
