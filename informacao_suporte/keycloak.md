---
layout: default
title: Entendendo conceitos de segurança para nossa aplicação! 
parent: Informação Suporte
---
# Entendendo conceitos de segurança para nossa aplicação!

## Contexto

Armazenar senhas e dados sensíveis sempre é uma missão crítica para sistemas. Essas informações são passíveis de auditoria e em alguns casos podemos ter vazamentos de informações, pelo fato de não estarmos preparados para **todos** os tipos de ataques que estamos sujeitos. Levando isso em conta, nosso processo de autenticação deve ser **delegado** a um sistema externo.

## Explicacao Necessária

Existe uma categoria de sistemas que lidam especificamente com gerenciamento e perfis de usuário. Nessa categoria, esses sistemas implementam de maneira bastante efetiva controles de segurança, criptografia da informação, proteção contra ataques comuns no mundo virtual. Eles contam com uma vasta variedade de features que você pode gradualmente aumentando ou reduzindo a segurança de controle de seus usuários.

Na nossa solução vamos usar a implementação do Keycloak, uma aplicação que pode nos ajudar a manter os dados dos nossos usuários seguros, além de prover uma maneira bem simples de integração com Spring Framework. O produto é open-source então podemos usá-lo sem nenhum problema de licenciamento. Aliás esse é um ponto de atenção: sempre utilize software de acordo com a regulamentação da licença


## Necessidades

Devemos "subir" nosso servidor de IAM e verificar se ele está operante e pronto para realizarmos nossas integrações que serão realizadas nos próximos passos.

## Resultado Esperado
- Identificar o serviço declarado no docker-compose.yaml
- Verificar a porta que o serviço esta exposto
- Logar no nosso IAM, escolhemos o Keycloak para este fim

## Informações de suporte
 
* Pode ser que seja sua primeira vez que você tenha se deparado com o termo _IAM_, 
não tem problema, [aqui você pode encontrar uma descrição sobre isso](https://www.gartner.com/en/information-technology/glossary/identity-and-access-management-iam)
  
  * Talvez você esta se perguntando existe uma outra fonte que pode me ajudar com isso?? Sim, este conteúdo foi produzido
  por uma companhia que criou uma implementação de IAM. [Aqui você pode encontrá-lo](https://www.okta.com/identity-101/federated-identity-vs-sso/)
  
  * Ou talvez você possa ter ouvido o termo SSO. [Aqui você pode encontrar a diferença entre esses dois termos](https://searchsecurity.techtarget.com/definition/federated-identity-management) 
    * Se você nunca ouviu o termo SSO e gostaria de se aprofundar um pouco. [Esse link pode te ajudar](https://www.cloudflare.com/learning/access-management/what-is-sso/)

* Em algum momento, você deve estar preocupado sobre licenças, não tem problema!! [Aqui voce encontra um link com tipos de licenças e suas descrições](https://opensource.org/licenses)        

* Se você esta se perguntando "O que é o keycloak???". [Esse link da documentação oficial pode te ajudar](https://www.keycloak.org/)
  
  * O Keycloak também faz parte do portfólio de projetos da CNCF, uma espécie de catálogo que nos ajuda escolher
   ferramentas que nos ajudam a trabalhar com aplicaçãoes Cloud-native. [Aqui você pode encontrar o detalhamento](https://landscape.cncf.io/selected=keycloak)
   
    * Você pode estar se perguntando, não sei o que é a CNCF. [Esse link pode tirar sua dúvida!!!](https://www.cncf.io/)  
  
  * Mas você pode estar se pergutando, se o projeto é open-source cade o github dele. [Aqui está o link](https://github.com/keycloak/keycloak)   
  
  * Se você já tem conhecimento sobre o que é IAM e tá afim de começar a utilizá-lo, [esse link pode te ajudar](https://www.keycloak.org/docs/latest/getting_started/index.html)  
    
    * Nós do Academy já deixamos uma instância preparada para você, se você usou nosso docker-compose.yaml. 
    [Esse link vai te ajudar a logar na plataforma](keycloak-login.md) 
      
      * [Aqui você encontra o nosso docker-compose.yaml](../informacao_procedural/nosso-compose.md) como uma série de serviços necessários para nossa solução!
    
    * Talvez você pode estar se perguntando o que é docker-compose. [Este link pode ter ajudar a entender melhor a ferramenta](https://docs.docker.com/compose/) 
