# SpringSecurity

Spring Boot Security + Jwt

Este projeto tem como objetivo a criação de um sistema para autenticação por meio de um usuário e senha e autorização por meio de um Token jwt codificado gerado após o processo de autenticação. O Spring Security é um framework  do spring que possibilita a criação de um sistema para autenticação e autorização customizável. Já o Jwt (Json Web Token) é um padrão para transmitir ou armazenar de forma compacta e segura objetos JSON.
JWT
O Jwt é normalmente utilizado para processo de autorização ou troca de informações de forma segura, pois permite uma assinatura digital por meio de um algoritmo ou por meio de um par de chaves pública/privada para codificar a mensagem.
O JWT tem a estrutura:
    * Header: informações do algoritmo de assinatura e tipo do token;
    * Payload: informações do usuário(CLAIMS) como nome e id; 
    * Signature: é o header e Payload codificados divididos por um “.”;

Exemplo de um JWT token com assinatura HS256 um dos mais de 10 algoritmos disponíveis:
![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/601ef251-a497-4212-9158-beaa3d97d979)

## Header
![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/85c3fa6b-34d6-427d-8400-6b666151cb4a)

“typ “:tipo do token
“alg”:algorítmo de criptografia 

## Payload
![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/581fe0d0-d173-492f-a6bc-18eaa977dc7d)


![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/727a70d5-3e5f-40e6-bc4f-745034b53b09)

Quando usamos Jwt Token para processo de autorização, o token é enviado através do header da solicitação http no campo Authorization com o prefixo “Bearer “ 
![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/d6535e62-512a-4993-99df-f4bfd3af98cc)

## Estrutura
    1. Classe UserDatailsImp que implementa a interface UserDetails
    2. Classe UserDetailsServiceImp que implementa a interface UserDetailsService
    3. Classe Spring Configuration
    4. Repositório que estende a classe JpaRepository
    5. Classe JwtUtils
    6. JwtTokenFilter que estende a classe OncePerRequestFilter
    7. Classe AuthEntryPointJwt que implementa a interface AutenticationEntryPoint

## Classe UserDetails e UserDetailsService
A classe UserDetailsService tem somente um método que é o LoadUserByUsername que tem a função de procurar os dados do usuário em um repositório e retorna um UserDetails com os dados do usuário.

## Spring Configuration
Essa classe é responsável por configurar o spring security como, por exemplo, definir o ProviderManager, Encoder e Decoder. O AuthenticationManager tem o método authentication que assume o papel de autenticar o usuário, mas repassa essa função para o ProviderManager que realiza a autenticação de acordo com o tipo definido, existe diversos tipos de autenticação já pronto, mas case precise você pode configurar o seu próprio ProviderManager, o método aqui utilizado foi o DaoAuthenticationProvider que é uma implementação do AuthenticationProvider que usa um UserDetailsService e PasswordEncoder para autenticar um username e password.

![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/9fb2289a-7d37-47c9-85bd-b443b471512a)

## Repositório
É a classe responsável por todas as operações no banco de dados, essa classe estende a classe JpaRepository que possui métodos definidos como o save(Objeto) que é responsável por salvar um objeto no banco de dados, mas o spring tem a habilidade de identificar alguns prefixos e criar a query de consulta, o prefixo FindBy indica ao spring que será feito um select no banco de dados, exemplo FindByUsername(String Username) indica ao spring que será feito um select com base no Username é preciso que no objeto de consulta tenha a variável que será usado como consulta.

## JwtUtils
Nessa classe definimos métodos para a construção do token jwt e mecanismos para validação do token, como por exemplo, verificar se o token não expirou.

## JwtTokenFilter
Essa classe é chamada sempre que uma requisição é feita, sua função é verificar se o usuário está autenticado e quais as autorizações ele possui.
 
## AutenticationEntryPoint
Classe responsável por  solicitar as credenciais ao cliente.

## SecurityContex
É o coração do modelo de autenticação do spring é onde o spring armazena os detalhes de quem está autenticado.

![image](https://github.com/And3rsoon/SpringSecurity/assets/114175542/7d6994f4-56a5-4604-84b3-38e427609a30)


