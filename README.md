# LiveTalk

---

### 1. **Estrutura Geral do Projeto**

```
LiveTalk Project

│
├── /frontend (React ou Vue.js)
│   │
│   ├── /components
│   │   ├── ChatBubble.js
│   │   └── VideoPlayer.js
│   │
│   ├── /views
│   │   ├── LoginPage.js
│   │   ├── ChatPage.js
│   │   └── VideoCallPage.js
│   │
│   ├── /services
│   │   ├── chatService.js
│   │   └── videoCallService.js
│   │
│   └── /styles
│       └── main.css
│
├── /backend (Node.js + MySQL + WebSockets)
│   │
│   ├── app.js (Servidor Principal)
│   │
│   ├── /routes
│   │   ├── authRoutes.js
│   │   └── messageRoutes.js
│   │
│   ├── /models
│   │   ├── userModel.js
│   │   └── messageModel.js
│   │
│   ├── /controllers
│   │   ├── authController.js
│   │   └── messageController.js
│   │
│   ├── /socket
│   │   ├── chatSocket.js
│   │   └── videoSocket.js
│   │
│   └── /config
│       └── db.js
│
└── /database (MySQL)
    ├── users
    ├── messages
    └── video_calls
```

---

### 2. **Interação entre o Frontend e o Backend**

Aqui está como as coisas se conectam:

#### **Frontend**
- **Páginas Principais**: O frontend tem páginas como **LoginPage**, **ChatPage** e **VideoCallPage**. Nelas, o usuário interage com a interface para enviar mensagens ou iniciar chamadas de vídeo.
- **Componentes**: Como **ChatBubble** e **VideoPlayer**, que mostram as mensagens ou a tela de vídeo.
- **Serviços**: Arquivos como `chatService.js` e `videoCallService.js` são responsáveis por fazer as requisições para o backend e interagir com a API do servidor.

#### **Backend**
- O **Backend** é responsável por gerenciar dados e processar a lógica de autenticação, mensagens e chamadas.
- **Rotas**: Arquivos como `authRoutes.js` e `messageRoutes.js` definem como o frontend comunica-se com o backend para enviar/receber dados.
- **Modelos**: Como `userModel.js` e `messageModel.js`, onde definimos como os dados são estruturados no banco de dados (MySQL).
- **Controladores**: Como `authController.js` e `messageController.js`, que controlam as operações de login e envio de mensagens.
- **Sockets**: Arquivos como `chatSocket.js` e `videoSocket.js` lidam com a comunicação em tempo real via WebSocket (usando `socket.io`), permitindo chat e chamadas de vídeo instantâneas.

#### **Banco de Dados (MySQL)**
- **Tabelas**:
  - **users**: Armazena informações dos usuários (nome, e-mail, senha).
  - **messages**: Armazena o histórico de mensagens enviadas entre os usuários.
  - **video_calls**: Armazena as informações de chamadas de vídeo realizadas (quem chamou, quem atendeu, hora da chamada, etc.).

---

### 3. **Fluxo de Ações:**

1. **Autenticação (Login)**:
   - O usuário se autentica na **LoginPage** (frontend).
   - O frontend envia a requisição de login para o **authRoutes.js** (backend).
   - O backend verifica os dados no banco de dados **users** e responde ao frontend com um token JWT, permitindo o acesso às páginas subsequentes.

2. **Chat**:
   - O usuário acessa a **ChatPage** e começa a enviar mensagens.
   - O frontend envia as mensagens para o backend via uma API REST (ex: `messageRoutes.js`).
   - O backend salva as mensagens no banco de dados **messages** e envia de volta para o frontend para exibição.
   - O **chatSocket.js** envia e recebe as mensagens em tempo real, exibindo as mensagens instantaneamente para todos os usuários conectados.

3. **Chamada de Vídeo**:
   - O usuário acessa a **VideoCallPage** e clica para iniciar uma chamada.
   - O frontend se comunica com o backend usando **videoSocket.js** para sinalizar que a chamada está começando.
   - Usando **WebRTC**, o frontend cria uma conexão direta entre os navegadores dos usuários, permitindo que a chamada de vídeo aconteça.
   - O backend não transmite o vídeo, apenas gerencia a sinalização entre os dois navegadores.

---

### 4. **Visão Geral da Arquitetura**

Aqui está uma ilustração de como as partes se conectam:

```
Frontend (React)
   │
   │ (requisição HTTP ou WebSocket)
   │
   ▼

Backend (Node.js)
   │
   ├── AuthController (Login)
   ├── MessageController (Enviar/Receber Mensagens)
   ├── VideoSocket (Gerenciar Chamada de Vídeo)
   │
   │ (conexão com o banco)
   │
   ▼

MySQL Database
   │
   ├── users (usuários)
   ├── messages (mensagens)
   └── video_calls (chamadas de vídeo)
```

---

### 5. **A Comunicação em Tempo Real:**

- O WebSocket, implementado com **socket.io**, permite que os usuários troquem mensagens instantaneamente, sem precisar atualizar a página.
- O **chatSocket.js** no backend gerencia a troca de mensagens entre os clientes.
- O **videoSocket.js** gerencia os sinais de chamada de vídeo (iniciar, aceitar, recusar chamadas).

---

### Resumo:

1. **Frontend**: Onde o usuário interage com a aplicação (Login, Chat, Vídeo).
2. **Backend**: Responsável pela autenticação, controle de mensagens e gestão de chamadas de vídeo.
3. **Banco de Dados**: Armazena dados dos usuários, mensagens e informações de chamadas de vídeo.
4. **WebSocket (Tempo Real)**: Permite a troca de mensagens e comunicação de vídeo sem atrasos.

---

### 6. **bibliotecas necessárias** para rodar o projeto **LiveTalk**

#### **1. Frontend (Syncfusion e React.js)**

##### **Bibliotecas Necessárias para o Frontend:**

- **React**: Para construir a interface do usuário.
  ```bash
  npm install react react-dom
  ```

- **React Router**: Para gerenciar a navegação entre páginas (ex: LoginPage, ChatPage, VideoCallPage).
  ```bash
  npm install react-router-dom
  ```

- **Axios**: Para fazer requisições HTTP para o backend (ex: login, enviar/receber mensagens).
  ```bash
  npm install axios
  ```

- **Socket.IO Client**: Para comunicação em tempo real via WebSockets.
  ```bash
  npm install socket.io-client
  ```

- **Styled Components (ou qualquer outra solução de CSS)**: Para estilizar os componentes.
  ```bash
  npm install styled-components
  ```

- **WebRTC (para chamadas de vídeo)**: Não há uma biblioteca específica, já que o WebRTC é nativo nos navegadores, mas você pode usar **peerjs** ou **simple-peer** para facilitar a configuração da chamada de vídeo.
  ```bash
  npm install peerjs
  ```

##### **Outras bibliotecas úteis para o frontend:**

- **React Bootstrap ou Material UI**: Para componentes de UI prontos, como botões, formulários e layouts responsivos.
  ```bash
  npm install react-bootstrap
  ```
  ou
  ```bash
  npm install @mui/material @emotion/react @emotion/styled
  ```

---

#### **2. Backend (Node.js + Express + WebSockets + MySQL)**

##### **Bibliotecas Necessárias para o Backend:**

- **Express.js**: Framework para gerenciar as rotas HTTP e configurar o servidor.
  ```bash
  npm install express
  ```

- **MySQL2**: Para conectar e interagir com o banco de dados MySQL.
  ```bash
  npm install mysql2
  ```

- **Socket.IO Server**: Para habilitar a comunicação em tempo real com WebSockets.
  ```bash
  npm install socket.io
  ```

- **JWT (JSON Web Tokens)**: Para autenticação de usuários. Usado para criar tokens de autenticação.
  ```bash
  npm install jsonwebtoken
  ```

- **bcryptjs**: Para criptografar senhas dos usuários de forma segura.
  ```bash
  npm install bcryptjs
  ```

- **CORS**: Para lidar com as permissões de requisições entre domínios (cross-origin).
  ```bash
  npm install cors
  ```

- **dotenv**: Para gerenciar variáveis de ambiente, como configurações de banco de dados e tokens JWT.
  ```bash
  npm install dotenv
  ```

##### **Outras bibliotecas úteis para o backend:**

- **Multer**: Se você precisar de upload de arquivos (como fotos de perfil, por exemplo).
  ```bash
  npm install multer
  ```

- **Nodemon**: Para reiniciar automaticamente o servidor durante o desenvolvimento.
  ```bash
  npm install --save-dev nodemon
  ```

---

#### **3. Banco de Dados (MySQL)**

- **MySQL**: O MySQL em si não é uma biblioteca, mas você pode usar o **MySQL2** para se conectar e interagir com o banco de dados no backend.

  **Instalar o MySQL**:
  - Instale o MySQL em seu sistema operacional.
  - Configure o banco de dados e as tabelas manualmente ou com comandos SQL.

---

#### **4. WebRTC e Vídeo (Comunicação de Vídeo)**

- **PeerJS (opcional)**: Uma biblioteca simples para facilitar a integração do WebRTC.
  ```bash
  npm install peerjs
  ```

---

#### **Resumindo:**

Aqui estão as **principais bibliotecas necessárias** para rodar o projeto:

##### **Frontend:**
1. `react`
2. `react-router-dom`
3. `axios`
4. `socket.io-client`
5. `peerjs` (para WebRTC)
6. `styled-components` (ou uma solução de CSS)

##### **Backend:**
1. `express`
2. `mysql2`
3. `socket.io`
4. `jsonwebtoken`
5. `bcryptjs`
6. `cors`
7. `dotenv`
8. `nodemon` (opcional, para desenvolvimento)

#### **Banco de Dados:**
1. MySQL (não é uma biblioteca Node, mas você precisará instalá-lo no seu sistema).

Essas são as bibliotecas para construir esta aplicação.

---

### 7. **Estrutura do MySQL**

```
CREATE DATABASE live_talk;
USE live_talk;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255) UNIQUE,
  password VARCHAR(255)
);

CREATE TABLE messages (
  id INT AUTO_INCREMENT PRIMARY KEY,
  sender_id INT,
  receiver_id INT,
  message TEXT,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (sender_id) REFERENCES users(id),
  FOREIGN KEY (receiver_id) REFERENCES users(id)
);

CREATE TABLE video_calls (
  id INT AUTO_INCREMENT PRIMARY KEY,
  caller_id INT,
  receiver_id INT,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (caller_id) REFERENCES users(id),
  FOREIGN KEY (receiver_id) REFERENCES users(id)
);
```

---
