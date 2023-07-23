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

## 13. Express.js - Middlewares de Terceiros: Cors e Helmet

O Express.js é um popular framework para aplicativos web em Node.js. Ele oferece uma arquitetura simples e flexível para construir APIs e aplicativos web. Uma das principais características do Express é a capacidade de usar middlewares, que são funções que são executadas sequencialmente para lidar com as requisições HTTP. Middlewares de terceiros são módulos externos que adicionam funcionalidades extras ao Express, ajudando a simplificar tarefas comuns ou aprimorar a segurança. Vamos entender dois desses middlewares de terceiros: Cors e Helmet.

1. CORS (Cross-Origin Resource Sharing):

O CORS é um mecanismo de segurança implementado nos navegadores que impede solicitações de serem feitas a um domínio diferente daquele em que a página está sendo executada. Isso é conhecido como mesma origem (same-origin policy). No entanto, há cenários legítimos em que você deseja permitir que sua API seja acessada por outros domínios (origens). É aí que o middleware CORS entra em cena.

O pacote cors é um middleware de terceiros que permite configurar as opções de CORS para a sua aplicação Express.

Exemplo de uso:
````javascript
const express = require('express');
const cors = require('cors');
const app = express();

// Habilitando o CORS para todas as rotas
app.use(cors());

// Definindo opções específicas do CORS
const corsOptions = {
  origin: 'https://meuapp.com', // Permitir apenas requisições desse domínio
  methods: ['GET', 'POST'], // Permitir apenas os métodos GET e POST
};

app.use('/api', cors(corsOptions));

// Rotas da API
app.get('/api/data', (req, res) => {
  res.json({ message: 'Dados da API' });
});

app.post('/api/create', (req, res) => {
  // Lógica para criar um novo recurso na API
});

app.listen(3000, () => {
  console.log('Servidor rodando na porta 3000');
});
````
2. Helmet:
O pacote helmet é outro middleware de terceiros que ajuda a melhorar a segurança da aplicação Express, configurando vários cabeçalhos HTTP relacionados à segurança.
````javascript
const express = require('express');
const helmet = require('helmet');
const app = express();

// Usando o middleware Helmet
app.use(helmet());

// Rotas da aplicação
app.get('/api/data', (req, res) => {
  res.json({ message: 'Dados da API' });
});

app.listen(3000, () => {
  console.log('Servidor rodando na porta 3000');
});
````
O middleware Helmet configura automaticamente os cabeçalhos HTTP, como:

X-Content-Type-Options: Define a opção "nosniff" para ajudar a evitar ataques baseados em MIME.
X-Frame-Options: Configura o cabeçalho "X-Frame-Options" para prevenir ataques de clique em link (clickjacking).
Strict-Transport-Security: Define a política de segurança de transporte para evitar ataques man-in-the-middle e forçar o uso de HTTPS.
Esses são apenas dois exemplos de middlewares de terceiros que podem ser usados em conjunto com o Express para adicionar funcionalidades adicionais ou aumentar a segurança da sua aplicação. O ecossistema do Node.js é rico em bibliotecas e pacotes, e você pode encontrar outros middlewares de terceiros que se adequem às necessidades específicas do seu projeto. Sempre verifique a documentação oficial dos pacotes para entender como usá-los corretamente.

## 13. Express.js - Objeto de resposta
A) res.download(): Envia um arquivo para ser salvo pelo cliente.
````javascript
const express = require('express');
const app = express();

app.get('/download', (req, res) => {
  const filePath = '/path/to/file.txt'; // Caminho do arquivo que será enviado para download
  res.download(filePath);
});

app.listen(3000);
````
B) res.end(): Finaliza o processo de resposta.
````javascript
const express = require('express');
const app = express();

app.get('/end', (req, res) => {
  res.end('Processo finalizado.');
});

app.listen(3000);
````

C) res.json(): Envia um objeto JSON como resposta.
````javascript
const express = require('express');
const app = express();

app.get('/json', (req, res) => {
  const data = { message: 'Exemplo de resposta JSON.' };
  res.json(data);
});

app.listen(3000);
````
D) res.jsonp(): Envia um objeto JSON como resposta no formato JSONP.

````javascript
const express = require('express');
const app = express();

app.get('/jsonp', (req, res) => {
  const data = { message: 'Exemplo de resposta JSONP.' };
  res.jsonp(data);
});

app.listen(3000);
````
E) res.redirect(): Redireciona uma requisição para outro recurso.
````javascript
const express = require('express');
const app = express();

app.get('/redirect', (req, res) => {
  res.redirect('https://www.example.com');
});

app.listen(3000);
````

F) res.render(): Processa um arquivo de template.

````javascript
const express = require('express');
const app = express();

app.set('view engine', 'ejs'); // Define o mecanismo de template como EJS

app.get('/render', (req, res) => {
  const data = { message: 'Exemplo de resposta renderizada.' };
  res.render('template', data); // Supondo que exista um arquivo "template.ejs"
});

app.listen(3000);
````
G) res.send(): Envia resposta de diversos tipos.

````javascript
const express = require('express');
const app = express();

app.get('/send', (req, res) => {
  res.send('<h1>Exemplo de resposta enviada.</h1>'); // Pode enviar HTML, texto, etc.
});

app.listen(3000);
````
H) res.sendFile(): Envia um arquivo como stream.

````javascript
const express = require('express');
const path = require('path');
const app = express();

app.get('/file', (req, res) => {
  const filePath = '/path/to/file.pdf'; // Caminho do arquivo que será enviado
  res.sendFile(path.join(__dirname, filePath));
});

app.listen(3000);
````
I) res.sendStatus(): Define o código de status da resposta e envia a mensagem de status padrão associada a ele.

````javascript
const express = require('express');
const app = express();

app.get('/status', (req, res) => {
  res.sendStatus(404); // Envia uma resposta com código de status 404 (Not Found)
});

app.listen(3000);
````

J) res.status(): Informa o código de status da resposta. O método status() permite o encadeamento de outras funções.
````javascript
const express = require('express');
const app = express();

app.get('/status', (req, res) => {
  res.status(200).json({ message: 'Exemplo de resposta com status 200.' });
});

app.listen(3000);
````
L) res.type(): Informa o tipo de conteúdo da resposta (definido no header Content-Type).

````javascript
const express = require('express');
const app = express();

app.get('/content', (req, res) => {
  res.type('text/plain'); // Define o tipo de conteúdo como texto plano
  res.send('Exemplo de resposta com tipo de conteúdo definido.');
});

app.listen(3000);
````
M) res.format(): Verifica o formato solicitado e envia a resposta apropriada (header Accept).
````javascript
const express = require('express');
const app = express();

app.get('/format', (req, res) => {
  res.format({
    'text/plain': () => {
      res.send('Resposta em texto plano.');
    },
    'application/json': () => {
      res.json({ message: 'Resposta em JSON.' });
    },
    'text/html': () => {
      res.send('<h1>Resposta em HTML.</h1>');
    },
  });
});

app.listen(3000);
````
## 14. Express.js - Objeto de Requisição
Lembre-se de instalar as dependências necessárias, como o body-parser e o cookie-parser, utilizando o npm ou yarn, antes de executar os exemplos abaixo.

A) req.body: Contém pares chave-valor com os dados submetidos no corpo da requisição.
Para usar req.body, é necessário configurar um middleware de parsing de corpo, como o body-parser ou o express.json(), no seu aplicativo Express.

Exemplo com body-parser:
````javascript
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

// Middleware para fazer o parsing do corpo da requisição
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

app.post('/data', (req, res) => {
  const data = req.body;
  console.log(data); // Exibe os dados enviados no corpo da requisição
  res.send('Dados recebidos com sucesso!');
});

app.listen(3000);
````
B) req.cookies: Contém os cookies enviados na requisição.
Para usar req.cookies, é necessário configurar um middleware cookie-parser no seu aplicativo Express.

Exemplo com cookie-parser:

````javascript
const express = require('express');
const cookieParser = require('cookie-parser');
const app = express();

// Middleware para fazer o parsing dos cookies da requisição
app.use(cookieParser());

app.get('/get-cookie', (req, res) => {
  const cookieData = req.cookies;
  console.log(cookieData); // Exibe os cookies enviados na requisição
  res.send('Cookies recebidos com sucesso!');
});

app.listen(3000);
````
C) req.host, req.hostname, req.ip, req.protocol: Contém as informações de host, hostname, IP e protocolo associados à requisição.
````javascript
const express = require('express');
const app = express();

app.get('/info', (req, res) => {
  console.log(`Host: ${req.host}`);
  console.log(`Hostname: ${req.hostname}`);
  console.log(`IP: ${req.ip}`);
  console.log(`Protocol: ${req.protocol}`);

  res.send('Informações da requisição exibidas no console.');
});

app.listen(3000);
````
D) req.params: Contém os parâmetros de path na URL da requisição.
````javascript
const express = require('express');
const app = express();

app.get('/produtos/:id', (req, res) => {
  const productId = req.params.id;
  console.log(`ID do produto: ${productId}`);
  res.send(`Produto com ID ${productId} encontrado.`);
});

app.listen(3000);
````
E) req.query: Contém os dados passados pela query string na URL da requisição.
````javascript
const express = require('express');
const app = express();

app.get('/produtos', (req, res) => {
  const sortBy = req.query.sort || 'asc';
  console.log(`Ordenar por: ${sortBy}`);
  res.send(`Lista de produtos ordenada por: ${sortBy}`);
});

app.listen(3000);
````
F) req.path: Contém a parte do path da URL.
````javascript
const express = require('express');
const app = express();

app.get('/user/profile', (req, res) => {
  console.log(`Path da URL: ${req.path}`);
  res.send('Exemplo de uso do req.path.');
});

app.listen(3000);
````
G) req.url: Contém a URL completa (path + query string).
````javascript
const express = require('express');
const app = express();

app.get('/search', (req, res) => {
  console.log(`URL completa: ${req.url}`);
  res.send('Exemplo de uso do req.url.');
});

app.listen(3000);
````
H) req.accepts(): Verifica se um determinado tipo de conteúdo é aceito pelo cliente.
````javascript
const express = require('express');
const app = express();

app.get('/data', (req, res) => {
  if (req.accepts('json')) {
    res.json({ message: 'Resposta em JSON aceita.' });
  } else if (req.accepts('html')) {
    res.send('<h1>Resposta em HTML aceita.</h1>');
  } else {
    res.status(406).send('Not Acceptable');
  }
});

app.listen(3000);
````
I) req.get(): Obtém um cabeçalho específico da requisição.
````javascript
const express = require('express');
const app = express();

app.get('/referrer', (req, res) => {
  const referrerHeader = req.get('Referrer');
  console.log(`Referrer: ${referrerHeader}`);
  res.send('Exemplo de uso do req.get() para obter o cabeçalho "Referrer".');
});

app.listen(3000);
````
