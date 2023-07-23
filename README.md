# Passo-a-passo para criar uma aplicação Express

## 1. Crie uma pasta para o projeto
Primeiro, crie uma pasta no local de sua escolha para armazenar os arquivos do seu projeto.

## 2. Abra a pasta no Visual Studio Code
Abra o Visual Studio Code (ou o editor de código de sua preferência) e navegue até a pasta que você criou anteriormente. Certifique-se de que você está trabalhando dentro dessa pasta ao longo de todo o processo.

## 3. Abra o terminal
No Visual Studio Code, clique em "Terminal" no menu superior e selecione "Novo Terminal" para abrir um terminal dentro do próprio editor.

## 4. Inicialize o projeto Node.js
Para iniciar um novo projeto Node.js, no terminal, digite o seguinte comando:
````javascript
npm init -y
````
O comando npm init é usado para criar um novo arquivo package.json na pasta do projeto. A opção -y indica que queremos usar as configurações padrão, sem a necessidade de responder a perguntas adicionais.

## 5. Instale o Express
Agora, vamos instalar o Express no projeto. No terminal, digite o seguinte comando:
````javascript
npm install express
````
Isso instalará o Express no seu projeto, permitindo que você use esse framework para construir a aplicação.

## 6. Crie o arquivo index.js
Dentro da pasta do projeto, crie um arquivo chamado index.js (você pode escolher outro nome, mas neste exemplo, usaremos index.js). Esse será o arquivo onde você escreverá o código principal da sua aplicação.

## 7. Escreva o código do servidor
Abra o arquivo index.js no editor e adicione o seguinte código:
````javascript
const express = require('express');
const app = express();

const mid = (req, res) => {
  res.send("Hello World Node.js community!");
};

app.get('/', mid);

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
````
Neste código, você importou o módulo express, criou uma instância do aplicativo Express e definiu uma rota para a raiz (/) que responde com a mensagem "Hello World Node.js community!".

## 8. Inicie o servidor
Para iniciar o servidor Express e executar a aplicação, vá até o terminal e digite o seguinte comando:
````javascript
node index.js
````
O servidor será iniciado e você verá a mensagem "Server is running on http://localhost:3000" no terminal.

## 9. Utilizando o Express Generator (Opcional)
O Express Generator é uma ferramenta útil para criar rapidamente a estrutura básica de um projeto Express. Se você preferir usar o Express Generator, siga estes passos:

Instale o Express Generator
No terminal, digite o seguinte comando:
````javascript
npm install express-generator -g
````
O parâmetro -g significa que estamos instalando o Express Generator globalmente, tornando-o acessível de qualquer lugar no sistema.
Crie o projeto usando o Express Generator
Ainda no terminal, navegue até a pasta onde você deseja criar o projeto e digite:
````javascript
npx express nome-do-seu-projeto
````
Substitua "nome-do-seu-projeto" pelo nome que você deseja dar ao seu projeto. O comando npx é usado para executar pacotes instalados localmente, como o Express Generator, sem a necessidade de instalá-los globalmente.

Instale as dependências e inicie o servidor
Navegue até a pasta do projeto recém-criado no terminal e execute os seguintes comandos:
````javascript
npm install
npm start
````
O primeiro comando irá instalar todas as dependências do projeto (incluindo o Express), e o segundo comando irá iniciar o servidor.

## 10. Padrão Middleware (tratamento de rota)
O padrão Middleware é uma abordagem comum em aplicações web para processar requisições antes que elas cheguem ao tratamento final da rota. Isso permite a execução de ações intermediárias, como validações, registros de logs ou autenticação, antes de prosseguir para o tratamento principal da rota.

No arquivo index.js, você pode implementar o padrão Middleware usando o framework Express. Vamos entender o código fornecido:
````javascript
const express = require('express');
const app = express();

app.get('/', (req, res, next) => {
    console.log(new Date().toLocaleDateString(), req.method, req.path);
    next(); // <-- Correção aqui: troque "nrxt()" por "next()"
});

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.get('*', (req, res) => {
    res.status(404).send('Recurso não encontrado');
});

app.listen(3000, () => {
    console.log('Server is running on http://localhost:3000');
});
````
Neste exemplo, criamos um Middleware personalizado que registra os detalhes da requisição, como data, método e caminho da requisição. Em seguida, chamamos next() para permitir que a requisição continue para a próxima função de tratamento de rota.

Em seguida, temos um tratamento de rota para a rota '/', que responde com o texto "Hello World!" quando essa rota é acessada.

Por fim, temos um tratamento de rota curinga ('*'), que é acionado quando nenhuma das rotas anteriores corresponde à requisição. Nesse caso, retornamos um código de status 404 (recurso não encontrado) como resposta.

Ao utilizar o padrão Middleware, você pode adicionar mais funções de tratamento intermediárias antes do tratamento final da rota, tornando sua aplicação mais modular e fácil de manter.

## 11. Middleware Static - Servindo Arquivos Estáticos
O middleware static é uma funcionalidade importante no Express que permite servir arquivos estáticos, como HTML, CSS, JavaScript, imagens e outros recursos, diretamente para o cliente, sem a necessidade de configurar rotas específicas para cada arquivo.

````javascript
const express = require('express');
const app = express();

app.get('/', (req, res, next) => {
    console.log(new Date().toLocaleDateString(), req.method, req.path);
    next(); // <-- Correção aqui: troque "nrxt()" por "next()"
});

app.use (express.static ('public'))

app.listen(3000, () => {
    console.log('Server is running on http://localhost:3000');
});
````
criar um arquivo index.html dentro da pasta public:
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Página Inicial</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 100px;
        }
        h1 {
            color: #007BFF;
        }
    </style>
</head>
<body>
    <h1>Bem-vindo à Página Inicial</h1>
    <p>Essa é uma página inicial simples criada com HTML e CSS.</p>
</body>
</html>
````
O middleware static é usado para fornecer conteúdo estático ao usuário sempre que uma solicitação é feita. Ao utilizar o express.static('public'), estamos instruindo o Express a procurar os arquivos dentro da pasta 'public' e enviá-los como resposta à solicitação do cliente.

Por exemplo, quando um usuário acessa a rota principal '/' do servidor, o middleware personalizado de registro de logs é executado primeiro, registrando detalhes sobre a requisição. Em seguida, o middleware static entra em ação, procurando o arquivo index.html dentro da pasta 'public' e enviando-o como resposta para a rota principal.

Dessa forma, sempre que você acessar http://localhost:3000, a página inicial index.html será exibida no navegador sem a necessidade de configurar uma rota específica para isso. O middleware static automatiza o processo de servir arquivos estáticos, tornando o desenvolvimento de aplicações web mais eficiente e organizado.

## 12. Middleware de Parses
No Express, os middlewares de parses são responsáveis por processar os dados do corpo (body) das requisições com base no tipo de conteúdo que está sendo enviado, como JSON, urlencoded, raw ou texto. Esses middlewares populam o objeto req.body com os dados processados, tornando-os acessíveis para uso posterior nas rotas.

````javascript
const express = require('express');
const app = express();

// Middleware para habilitar o uso de JSON nas requisições POST
app.use(express.json());

// Middleware para registro de logs
app.use((req, res, next) => {
    console.log(new Date().toLocaleDateString(), req.method, req.path);
    next();
});

// Middleware Static para servir arquivos da pasta 'public'
app.use('/site', express.static('public'));

app.post('/users', (req, res) => {
    const dados = req.body;
    console.log(dados);
    res.send('Informação recebida com sucesso');
});

app.listen(3000, () => {
    console.log('Server is running on http://localhost:3000');
});
````
Explicação:

Middleware express.json(): Este middleware é usado para tratar dados enviados no formato JSON. Quando você envia uma requisição POST com o cabeçalho "Content-Type: application/json", o Express irá utilizar esse middleware para analisar o corpo da requisição e converter o JSON em um objeto JavaScript, que é acessível através da propriedade req.body.

Middleware express.urlencoded(): Esse middleware é usado para tratar dados enviados no formato URL-encoded. Quando você envia uma requisição POST com o cabeçalho "Content-Type: application/x-www-form-urlencoded", o Express utilizará esse middleware para analisar o corpo da requisição e transformar os dados em um objeto JavaScript, que é acessível através da propriedade req.body.

Middleware express.raw(): Este middleware é usado para tratar dados enviados no formato raw (cru), ou seja, dados binários ou de texto não estruturado. Ele coloca os dados brutos no corpo da requisição na propriedade req.body.

Middleware express.text(): Esse middleware é usado para tratar dados enviados no formato de texto simples. Quando você envia uma requisição POST com o cabeçalho "Content-Type: text/plain", o Express utilizará esse middleware para analisar o corpo da requisição e colocar o texto na propriedade req.body.

Para testar os middlewares, você pode utilizar a extensão Thunder Client no Visual Studio Code para simular requisições.

Exemplo de requisição GET:

Digite o seguinte endereço utilizando o método GET e veja o resultado:

URL: http://localhost:3000/site

Resultado: Se houver algum arquivo correspondente na pasta 'public' em relação à rota '/site', ele será servido pelo middleware static. Caso contrário, retornará um erro 404 Not Found.

Exemplo de requisição POST:

Digite o seguinte endereço utilizando o método POST e veja o resultado:

URL: http://localhost:3000/users

Corpo da Requisição (JSON):
````json
{
  "nome": "João",
  "idade": 30
}
````
Resultado: O middleware express.json() irá processar o corpo da requisição no formato JSON, e o objeto req.body será preenchido com os dados enviados. O servidor irá imprimir os dados recebidos no console e enviará a resposta "Informação recebida com sucesso" de volta ao cliente.
