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
