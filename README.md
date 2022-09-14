<h1 align="center">
    Code Challenge
</h1>



#### Estrutura da collection

![image](https://user-images.githubusercontent.com/35806393/190032212-97e3fbdb-5127-493b-b8e0-080c28946496.png)

### Explicação do projeto

O projeto tem por objetivo fazer as validações na API conforme o challenge, além dos cenários de negócio também foi criado cenários que visa seguir as boas práticas para desenvolvimentos de APIs Rest. 

### Utilização do postman para automatizar os testes

O Postman com certeza é uma das ferramentas mais utilizada pelo o time de desenvolvimento, qualidade e até mesmo de negócio, por sua facilidade de fazer uma validação rápida em uma API. Além desse recurso o postman conta com outros recursos bem bacana, por exemplo, é a criação do mock server!

Porém, mesmo o postman sendo tão bom ele deixa a desejar um pouco quando falamos de boas práticas de automação, por não ser uma ferramenta voltado 100% para automação criar cenários e utilizar o gherkin no postman já não é possível, acabamos tendo que replicar muita linha de código, pois pra cada cenário que utilizamos temos que criar uma request.

Por exemplo, na collection tem um cenário de testes que fazemos a validação da obrigatoriedade dos campos, onde temos por volta de 4 campos obrigatórios... No postman temos que criar um cenário para cada campo, já no cucumber poderíamos criar um cenário e dentro dele inserirmos um datatable. 
> 
```
Esquema do Cenario: Verificar mensagens obrigatórias
    Dado que feito um POST sem passar o <atributo>
    Então é retornado a <mensagem>
    Exemplos:
        | atributo   | mensagem                 | 
        | "name"     | "name é obrigatório"     |
        | "power"    | "power é obrigatório"    |
        | "velocity" | "velocity é obrigatório" |
```      
Olhando o gherkin acima diminuiriamos a quantidade de linha de código e de cenário de testes sendo que para cada linha do datatable seria um cenário de teste que teriamos que criar no postman.

### Pre Request Script
Na estrutura do código estou utilizando o pre request script para executar a chamada do token e dos cenários de testes que precisam de pré execução antes de rodar o request.

### BUGS
Identifiquei alguns bugs durante minhas automações.

Bug 1 - no cenário da automação é validado para retornar o status 400 quando for deixado de ser passado algum campo obrigatório a aplicação retorna um 500 internal server error, na boa práticas de status code devemos usar a família 4x para erro de request do usuário, como o usuario deixou de passar um atributo obrigatório deveria retornar o status 400. Outro status que coloquei é o 401 caso o usuário tente criar herói duplicado, a aplicação esta retornando status 500.

Bug 2 - Ao passar um valor maior que 200 ele efetua o POST retornando no body o valor do atributo alterado com 200, como na imagem abaixo

![image](https://user-images.githubusercontent.com/35806393/190021133-1ac6fac3-18eb-40ad-a4fa-44da377d5c9a.png)

Bug 3 - Esta gravando valores menores do que 0

![image](https://user-images.githubusercontent.com/35806393/190021172-55b0c1ce-a836-4759-b039-3a30debc447e.png)

Bug 4 - Não grava quando um queremos criar um herói que tenha alguma skill = 0

![image](https://user-images.githubusercontent.com/35806393/190021207-b449f33f-e1f6-4321-9701-c66c628de4da.png)
 
 Bug 5 - Payload incorreto na documentação o endpoint recebe o atributo "combat" e não "combate"

![image](https://user-images.githubusercontent.com/35806393/190021376-8a5d074e-a1a4-47bf-a0fc-6545cb951e13.png)

### Rodando a collection
Para rodar a automação basta baixar a collection e a váriavel de ambiente do projeto e importar dentro do próprio postman


https://user-images.githubusercontent.com/35806393/190034814-7b4f1397-f588-42ab-a4f2-be20e8457e1e.mp4
