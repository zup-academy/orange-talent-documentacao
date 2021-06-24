---
layout: default
title: OAuth2 um padrão de mercado para segurança de APIs REST! 
parent: Informação Suporte
---
# OAuth2 um padrão de mercado para segurança de APIs REST!

Não queremos que qualquer usuário acesse nossa aplicação, por isso, precisamos de algum mecanismo que nos ajude a protegê-la.

Temos algumas maneiras de realizar essa tarefa: poderíamos usar o modelo mais simples com usuário e senha. Dessa maneira o usuário sempre que requisitar acesso a nossa aplicação deverá informar usuário + senha no Header da requisição.

Perceba que esse modelo não oferece uma segurança tão efetiva, porque em todos os requests informamos nossas credenciais, caso alguém consiga um acesso não autorizado a esses headers, nosso usuário e senha serão comprometidos.

Ainda existem alguns itens que precisam ser endereçados, como por exemplo, delegação de acesso.  Claramente o modelo Basic de Autenticação não suporta delegação, nessa situação você precisaria informar a senha do seu Facebook, Google ou Github em cada acesso a site de terceiros, isso não parece ser adequado.

Precisamos delegar o acesso, podemos usar nossa credencial de Google, Facebook e Github mas não queremos informar nossa senha para um site terceiro, esse site terceiro deve requisitar ao provedor e então podemos continuar com nossa autenticação. Perceba que todo processo de autenticação acontece no nosso provedor de autenticação. Não há em nenhum momento troca de informação de credenciais entre site terceiro e provedor de autenticação.

## Entendendo as entidades do OAuth2

Talvez você possa se perguntar se envolve delegação, então provavelmente tem mais de um sistema envolvido nesse mecanismo. Exatamente o fluxo OAuth2 é composto por 4 entidades principais [aqui você pode encontrar uma referência
oficial](https://tools.ietf.org/html/rfc6749#section-1.1) 

* Talvez alguns elementos do OAuth2 não tenha ficado perfeitamente claro, [aqui nós tentamos achar uma maneira mais
 simplificada de explicar as 4 entidades principais](../informacao_procedural/oauth2_entidades.md)

## IAM (Identity and Access Management)

Existe uma categoria de sistemas que lidam especificamente com gerenciamento e perfis de usuário. Nessa categoria, esses sistemas implementam de maneira bastante efetiva controles de segurança, criptografia da informação, proteção contra ataques comuns no mundo virtual. Eles contam com uma vasta variedade de features que você pode gradualmente aumentando ou reduzindo a segurança de controle de seus usuários.

Na nossa solução vamos usar a implementação do Keycloak, uma aplicação que pode nos ajudar a manter os dados dos nossos usuários seguros, além de prover uma maneira bem simples de integração com Spring Framework. O produto é open-source então podemos usá-lo sem nenhum problema de licenciamento. Aliás esse é um ponto de atenção sempre utilize software de acordo com a regulamentação da licença.

## Informações de suporte
 
* Se você está curioso em saber como funciona o método Basic de Autenticação HTTP, [nesse link você pode
encontrar aqui](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
