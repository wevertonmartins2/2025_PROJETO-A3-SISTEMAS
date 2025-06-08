# 🏥 Sistema de Clínica Médica - API RESTful

Este projeto implementa uma API RESTful completa para um sistema de gerenciamento de clínica médica, seguindo os princípios da arquitetura REST conforme descrito por Roy Fielding. O sistema permite realizar operações CRUD (Create, Read, Update, Delete) sobre diversas entidades relacionadas ao contexto de uma clínica médica, como pacientes, médicos, consultas, prontuários, exames e prescrições.

## 📚 Sumário

- 🔍 [ Visão Geral](#visão-geral)
- 📋 [Requisitos](#requisitos)
- 📁 [Estrutura do Projeto](#estrutura-do-projeto)
- ⚙️ [Configuração do Ambiente](#configuração-do-ambiente)
- 🗃️ [Banco de Dados](#banco-de-dados)
- 🔗 [Endpoints da API](#endpoints-da-api)
- 🔐 [Autenticação e Autorização](#autenticação-e-autorização)
- 🔄 [Coleção de Testes](#Coleção-de-Testes-no-Postman)
  - ✅ [Testes de Backend](#testes-de-backend)
- 🚀 [Executando o Projeto](#executando-o-projeto)
- 🛡️ [Considerações de Segurança](#considerações-de-segurança)
- 📈 [Melhorias Futuras](#melhorias-futuras)
- 👥 [Grupo A3](#Grupo-A3)

## 🔍Visão Geral

O sistema foi desenvolvido para atender às necessidades de uma clínica médica, permitindo o gerenciamento de pacientes, médicos, consultas, prontuários, exames e prescrições. A API segue os princípios da arquitetura REST, implementando todos os constraints definidos por Roy Fielding:

1. **Client-Server**: Separação clara entre cliente e servidor.
2. **Stateless**: Todas as requisições contêm todas as informações necessárias para o processamento.
3. **Cacheable**: As respostas contêm informações de cache (quando aplicável).
4. **Uniform Interface**: A interface da API é uniforme, seguindo convenções REST.
5. **Layered System**: A arquitetura permite o uso de camadas intermediárias.
6. **Code on Demand** (opcional): Possibilidade de envio de scripts executáveis ao cliente (se aplicável).

## 📋Requisitos

### Backend
- Node.js (v14.x ou superior)
- MySQL (v5.7 ou superior)
- npm ou yarn

## 📁Estrutura do Projeto

```
clinica-api/
├── src/
│   ├── config/                  → Configurações do banco
│   ├── controllers/             → Lógica de cada entidade
│   ├── middlewares/            → Middleware de autenticação
│   ├── models/                 → Definição das entidades (ORM)
│   ├── routes/                 → Definição de rotas da API
│   └── utils/                  → Scripts de banco e testes
├── .env                        → Variáveis de ambiente
├── package.json                → Dependências do projeto
└── server.js                   → Ponto de entrada da API

```
## ⚙️Configuração do Ambiente

### Backend

1 **Clone o repositório:**
   ```bash
   git clone https://github.com/seu-usuario/clinica-api.git
   cd clinica-api
   ```

2. **.Instale as dependências:**
   ```bash
   npm install
   ```
   
3. **.Configure o arquivo `.env` na raiz do projeto:**

   ```
   # Configurações do Servidor
   PORT=3000
   NODE_ENV=development

   # Configurações do Banco de Dados
   DB_HOST=localhost
   DB_USER=root
   DB_PASS=sua_senha
   DB_NAME=clinica_db

   # Configurações JWT
   JWT_SECRET=sua_chave_secreta
   JWT_EXPIRES_IN=1d
   ```

4. **Crie o banco de dados:**
   ```bash
   npm run db:create
   ```

5. **Popule o banco de dados com dados iniciais:**
   ```bash
   npm run db:seed
   ```
## 🗃️Banco de Dados

O sistema utiliza um banco de dados MySQL com as seguintes tabelas:

1. **Pacientes**: Armazena informações dos pacientes.
2. **Médicos**: Armazena informações dos médicos.
3. **Consultas**: Registra as consultas agendadas ou realizadas.
4. **Prontuários**: Armazena o histórico médico de um paciente.
5. **Exames**: Registra exames solicitados ou realizados.
6. **Prescrições**: Armazena prescrições médicas associadas a consultas.
7. **Usuários**: Armazena informações de usuários do sistema.

### Diagrama de Relacionamentos

- Pacientes ↔ Consultas (1:N): Um paciente pode ter várias consultas.
- Médicos ↔ Consultas (1:N): Um médico pode atender várias consultas.
- Consultas ↔ Exames (1:N): Uma consulta pode gerar vários exames.
- Consultas ↔ Prescrições (1:N): Uma consulta pode gerar várias prescrições.
- Pacientes ↔ Prontuários (1:N): Um paciente pode ter vários prontuários.
- Pacientes ↔ Exames (1:N): Um paciente pode realizar vários exames.
- Pacientes ↔ Prescrições (1:N): Um paciente pode receber várias prescrições.

## 🔗Endpoints da API

A API oferece os seguintes endpoints para cada entidade:

### 📍Base URL
```
http://localhost:3000/api
```

### 🔐Autenticação
- `POST /auth/login`: Autentica um usuário.
- `POST /auth/register`: Registra um novo usuário.

### 👤Pacientes
- `GET /pacientes`: Lista todos os pacientes (com paginação).
- `GET /pacientes/:id`: Obtém detalhes de um paciente.
- `POST /pacientes`: Cria um novo paciente.
- `PUT /pacientes/:id`: Atualiza um paciente existente.
- `PATCH /pacientes/:id`: Atualiza parcialmente um paciente.
- `DELETE /pacientes/:id`: Exclui um paciente.

### 👨‍⚕️Médicos
- `GET /medicos`: Lista todos os médicos.
- `GET /medicos/:id`: Obtém detalhes de um médico.
- `POST /medicos`: Cria um novo médico.
- `PUT /medicos/:id`: Atualiza um médico.
- `PATCH /medicos/:id`: Atualiza parcialmente um médico.
- `DELETE /medicos/:id`: Exclui um médico.

### 📅Consultas
- `GET /consultas`: Lista todas as consultas (filtros: ?id_paciente=1, ?id_medico=2, ?data_inicio=2025-06-01).
- `GET /consultas/:id`: Obtém detalhes de uma consulta.
- `POST /consultas`: Cria uma nova consulta.
- `PUT /consultas/:id`: Atualiza uma consulta.
- `PATCH /consultas/:id`: Atualiza parcialmente uma consulta.
- `DELETE /consultas/:id`: Cancela uma consulta.

### 📄Prontuários
- `GET /prontuarios`: Lista prontuários (filtro: ?id_paciente=1).
- `GET /prontuarios/:id`: Obtém um prontuário.
- `POST /prontuarios`: Cria um novo prontuário.
- `PUT /prontuarios/:id`: Atualiza um prontuário.
- `DELETE /prontuarios/:id`: Exclui um prontuário.

### 🧪Exames
- `GET /exames`: Lista exames (filtros: ?id_paciente=1, ?id_consulta=1).
- `GET /exames/:id`: Obtém detalhes de um exame.
- `POST /exames`: Cria um novo exame.
- `PUT /exames/:id`: Atualiza um exame.
- `PATCH /exames/:id`: Atualiza parcialmente um exame.
- `DELETE /exames/:id`: Exclui um exame.

### 💊Prescrições
- `GET /prescricoes`: Lista prescrições (filtros: ?id_paciente=1, ?id_consulta=1).
- `GET /prescricoes/:id`: Obtém detalhes de uma prescrição.
- `POST /prescricoes`: Cria uma nova prescrição.
- `PUT /prescricoes/:id`: Atualiza uma prescrição.
- `PATCH /prescricoes/:id`: Atualiza parcialmente uma prescrição.
- `DELETE /prescricoes/:id`: Exclui uma prescrição.

## 🔑Autenticação e Autorização

O sistema utiliza tokens JWT (JSON Web Tokens) para autenticação e controle de acesso baseado em papéis (RBAC).

### Papéis de Usuário
- **Admin**: Acesso total ao sistema.
- **Médico**: Acesso a consultas, prontuários, exames e prescrições.
- **Recepcionista**: Acesso a pacientes, médicos e consultas.

### Fluxo de Autenticação
1. O usuário faz login com email e senha.
2. O servidor valida as credenciais e gera um token JWT.
3. O cliente armazena o token e o inclui no cabeçalho `Authorization` em requisições subsequentes.
4. O servidor valida o token e verifica as permissões do usuário para cada operação.


## 🔄Coleção de Testes no Postman

#### 📁Testes de Backend
```
API Clínica
├── 🔐 Autenticação
│   ├── POST /auth/register
│   └── POST /auth/login
├── 👤 Pacientes
│   └── POST /pacientes
│   └── GET /pacientes
│   └── PUT /pacientes
│   └── DEL /pacientes


```
#####  🔐 1. Registro de Usuário
- Método: POST
- URL: http://localhost:3000/api/auth/register
- Body (JSON):
  
```postman
{
  "nome": "Usuário Teste",
  "email": "usuario.teste@clinica.com",
  "senha": "senha123",
  "role": "admin"
}

pm.test("✅ Registro - status 201", () => {
  pm.response.to.have.status(201);
});

pm.test("✅ Registro - formato da resposta", () => {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.have.property("status", "success");
  pm.expect(jsonData).to.have.property("message", "Usuário registrado com sucesso");
  pm.expect(jsonData.data).to.have.property("usuario");
  pm.expect(jsonData.data.usuario).to.include({
    nome: "Usuário Teste",
    email: "usuario.teste@clinica.com",
    role: "admin"
  });
  pm.expect(jsonData.data).to.have.property("token");
});

// Salvar token para as próximas requisições
pm.environment.set("token", pm.response.json().data.token);

```
##### 🔐 2. Login de Administrador

- Método: POST
- URL: http://localhost:3000/api/auth/login
- Body (JSON):
  
```postman
  {
    "email": "usuario.teste@clinica.com",
    "senha": "senha123"
  }
 pm.test("✅ Login - status 200", () => {
  pm.response.to.have.status(200);
});

pm.test("✅ Login - formato da resposta", () => {
  const jsonData = pm.response.json();
  pm.expect(jsonData).to.have.property("status", "success");
  pm.expect(jsonData).to.have.property("message", "Login realizado com sucesso");
  pm.expect(jsonData.data).to.have.property("usuario");
  pm.expect(jsonData.data.usuario).to.have.property("email", "usuario.teste@clinica.com");
  pm.expect(jsonData.data).to.have.property("token");
});

// Armazenar token no ambiente do Postman
pm.environment.set("token", jsonData.data.token);

```

#####  📌 Testes de Pacientes no Postman de CRUD

#####  ✅  1. Criar Novo Paciente📝

- Método: POST
- URL: http://localhost:3000/api/pacientes
- Headers:
```postman
{
  "Authorization": "Bearer {{token}}",
  "Content-Type": "application/json"
}
```
- Body (raw JSON):
```postman
{
  "nome": "Paciente Teste",
  "cpf": "111.222.333-44",
  "data_nascimento": "1990-01-01",
  "telefone": "(11) 98765-4321",
  "email": "paciente.teste@email.com",
  "endereco": "Rua Teste, 123 - Minas Gerais/MG"
}
```

#### 🔎 GET - Buscar Paciente por ID
- Método: GET
- URL: http://localhost:3000/api/pacientes/{{pacienteId}}
  
```postman
{
  "Authorization": "Bearer {{token}}"
}
pm.test("✅ GET - Status 200 OK", () => {
  pm.response.to.have.status(200);
});

const data = pm.response.json().data;

pm.test("✅ GET - Nome do paciente é Paciente Teste", () => {
  pm.expect(data.nome).to.eql("Paciente Teste");
});

pm.test("✅ GET - Verificar campos obrigatórios", () => {
  pm.expect(data).to.have.property("cpf");
  pm.expect(data).to.have.property("email");
  pm.expect(data).to.have.property("data_nascimento");
});
```

#### 📝 PUT - Atualizar Paciente
- Método: PUT
- URL:
  
```postman
http://localhost:3000/api/pacientes/{{pacienteId}}
```
- Headers:
```postman
{
  "Authorization": "Bearer {{token}}",
  "Content-Type": "application/json"
}
```
- Body (raw JSON):
```postman
{
  "nome": "Maria Santos",
  "cpf": "983.654.321-00",
  "data_nascimento": "1990-10-20",
  "telefone": "(11) 98765-4321",
  "email": "maria@email.com",
  "endereco": "Av. B, 456 - São Paulo/SP"
}

pm.test("✅ PUT - Status 200 OK", () => {
  pm.response.to.have.status(200);
});

const data = pm.response.json().data;

pm.test("✅ PUT - Paciente atualizado corretamente", () => {
  pm.expect(data.nome).to.eql("Maria Santos");
  pm.expect(data.email).to.eql("maria@email.com");
  pm.expect(data.updated_at).not.eql(data.created_at);
});

```

#### 🗑️ DELETE - Remover Paciente
- Método: DELETE
- URL:
  
```postman
http://localhost:3000/api/pacientes/{{pacienteId}}
```
- Headers:
```postman
{
  "Authorization": "Bearer {{token}}"
}

pm.test("✅ DELETE - Status 200 OK", () => {
  pm.response.to.have.status(200);
});

const jsonData = pm.response.json();

pm.test("✅ DELETE - Mensagem de sucesso", () => {
  pm.expect(jsonData.message).to.include("excluído");
});

pm.test("✅ DELETE - Retorno com status 'success'", () => {
  pm.expect(jsonData.status).to.eql("success");
});
```

## 🚀Executando o Projeto

### Backend

1. Inicie o servidor:
   ```bash
   cd clinica-api
   npm run dev
   ```
   O servidor estará disponível em `http://localhost:3000`.

## 🛡️Considerações de Segurança

O projeto implementa várias medidas de segurança:

1. **Autenticação com JWT**: Tokens JWT são utilizados para autenticar usuários.
2. **Controle de Acesso Baseado em Papéis (RBAC)**: Diferentes níveis de acesso são definidos para diferentes tipos de usuário.
3. **Validação de Dados**: Todos os dados de entrada são validados antes de serem processados.
4. **Proteção contra CSRF**: Tokens são utilizados para proteger contra ataques CSRF.
5. **Proteção contra SQL Injection**: O ORM Sequelize é utilizado para prevenir ataques de SQL Injection.
6. **Senhas Criptografadas**: As senhas são armazenadas de forma criptografada utilizando bcrypt.

## 📈Melhorias Futuras

Algumas melhorias que podem ser implementadas no futuro:

1. **Testes Automatizados para o Frontend**: Implementar testes automatizados para o frontend utilizando Jest e React Testing Library.
2. **Implementação de WebSockets**: Para notificações em tempo real.
3. **Melhorias na Interface do Usuário**: Adicionar mais recursos visuais e melhorar a experiência do usuário.
4. **Implementação de Relatórios**: Adicionar funcionalidades para geração de relatórios.
5. **Integração com Serviços de Email**: Para envio de notificações por email.
6. **Implementação de PWA**: Transformar o frontend em um Progressive Web App.
7. **Melhorias na Segurança**: Implementar autenticação de dois fatores e outras medidas de segurança adicionais.

## 🤝Contribuição

Contribuições são bem-vindas! Sinta-se à vontade.

## 👥Grupo A3
- Desenvolvido por:
  - EDILSON CLODOALVES GALVÃO DE LIMA - 32214931
  - FLÁVIO GREGO SANTIAGO - 322129707
  - WEVERTON ARAÚJO MARTINS - 32210007


