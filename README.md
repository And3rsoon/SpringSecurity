# SpringSecurity

Spring Boot Security + Jwt

Este projeto tem como objetivo a criação de um sistema para autenticação por meio de um usuário e senha e autorização por meio de um Token jwt codificado gerado após o processo de autenticação. O Spring Security é um framework  do spring que possibilita a criação de um sistema para autenticação e autorização customizável. Já o Jwt (Json Web Token) é um padrão para transmitir ou armazenar de forma compacta e segura objetos JSON.
JWT
O Jwt é normalmente utilizado para processo de autorização ou troca de informações de forma segura, pois permite uma assinatura digital por meio de um algoritmo ou por meio de um par de chaves pública/privada para codificar a mensagem.
O JWT tem a estrutura:
    • Header: informações do algoritmo de assinatura e tipo do token;
    • Payload: informações do usuário(CLAIMS) como nome e id; 
    • Signature: é o header e Payload codificados divididos por um “.”;

Exemplo de um JWT token com assinatura HS256 um dos mais de 10 algoritmos disponíveis:
![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/601ef251-a497-4212-9158-beaa3d97d979)
