# 🏥 Sistema de Clínica Médica - API RESTful

Este projeto implementa uma API RESTful completa para um sistema de gerenciamento de clínica médica, seguindo os princípios da arquitetura REST conforme descrito por Roy Fielding. O sistema permite realizar operações CRUD (Create, Read, Update, Delete) sobre diversas entidades relacionadas ao contexto de uma clínica médica, como pacientes, médicos, consultas, prontuários, exames e prescrições.

## 📚 Sumário

🔍- [ Visão Geral](#visão-geral)
- [Requisitos](#requisitos)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Configuração do Ambiente](#configuração-do-ambiente)
- [Banco de Dados](#banco-de-dados)
- [Endpoints da API](#endpoints-da-api)
- [Autenticação e Autorização](#autenticação-e-autorização)
- [Testes](#testes)
  - [Testes de Backend](#testes-de-backend)
  - [Testes de Frontend](#testes-de-frontend)
- [Frontend](#frontend)
- [Executando o Projeto](#executando-o-projeto)
- [Considerações de Segurança](#considerações-de-segurança)
- [Melhorias Futuras](#melhorias-futuras)

## Visão Geral

O sistema foi desenvolvido para atender às necessidades de uma clínica médica, permitindo o gerenciamento de pacientes, médicos, consultas, prontuários, exames e prescrições. A API segue os princípios da arquitetura REST, implementando todos os constraints definidos por Roy Fielding:

1. **Client-Server**: Separação clara entre cliente e servidor.
2. **Stateless**: Todas as requisições contêm todas as informações necessárias para o processamento.
3. **Cacheable**: As respostas contêm informações de cache (quando aplicável).
4. **Uniform Interface**: A interface da API é uniforme, seguindo convenções REST.
5. **Layered System**: A arquitetura permite o uso de camadas intermediárias.
6. **Code on Demand** (opcional): Possibilidade de envio de scripts executáveis ao cliente (se aplicável).

## Requisitos

### Backend
- Node.js (v14.x ou superior)
- MySQL (v5.7 ou superior)
- npm ou yarn

### Frontend
- Node.js (v14.x ou superior)
- npm ou yarn

## Estrutura do Projeto

O projeto está organizado em duas partes principais: backend (API) e frontend.

### Estrutura do Backend

```
clinica-api/
├── node_modules/
├── src/
│   ├── config/
│   │   └── database.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── pacienteController.js
│   │   ├── medicoController.js
│   │   ├── consultaController.js
│   │   ├── prontuarioController.js
│   │   ├── exameController.js
│   │   └── prescricaoController.js
│   ├── middlewares/
│   │   └── authMiddleware.js
│   ├── models/
│   │   ├── Paciente.js
│   │   ├── Medico.js
│   │   ├── Consulta.js
│   │   ├── Prontuario.js
│   │   ├── Exame.js
│   │   ├── Prescricao.js
│   │   ├── Usuario.js
│   │   └── index.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── pacienteRoutes.js
│   │   ├── medicoRoutes.js
│   │   ├── consultaRoutes.js
│   │   ├── prontuarioRoutes.js
│   │   ├── exameRoutes.js
│   │   └── prescricaoRoutes.js
│   ├── tests/
│   │   ├── api.test.js
│   │   ├── auth.test.js
│   │   ├── crud.test.js
│   │   └── setup.js
│   └── utils/
│       ├── createDatabase.js
│       ├── initializeDatabase.js
│       ├── seedDatabase.js
│       └── testDatabaseConnection.js
├── .env
├── .gitignore
├── jest.config.js
├── package.json
└── server.js
```

### Estrutura do Frontend

```
clinica-frontend/
├── node_modules/
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── Navbar.jsx
│   │   ├── ProtectedRoute.jsx
│   │   ├── Sidebar.jsx
│   │   └── ui/
│   ├── pages/
│   │   ├── Dashboard.jsx
│   │   ├── Login.jsx
│   │   ├── Pacientes.jsx
│   │   ├── Medicos.jsx
│   │   ├── Consultas.jsx
│   │   ├── Prontuarios.jsx
│   │   ├── Exames.jsx
│   │   └── Prescricoes.jsx
│   ├── services/
│   │   └── api.js
│   ├── App.css
│   ├── App.jsx
│   ├── index.css
│   └── main.jsx
├── .gitignore
├── index.html
├── package.json
└── vite.config.js
```

## Configuração do Ambiente

### Backend

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/clinica-api.git
   cd clinica-api
   ```

2. Instale as dependências:
   ```bash
   npm install
   ```

3. Configure o arquivo `.env` na raiz do projeto:
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

4. Crie o banco de dados:
   ```bash
   npm run db:create
   ```

5. Popule o banco de dados com dados iniciais:
   ```bash
   npm run db:seed
   ```

### Frontend

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/clinica-frontend.git
   cd clinica-frontend
   ```

2. Instale as dependências:
   ```bash
   npm install
   ```

## Banco de Dados

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

## Endpoints da API

A API oferece os seguintes endpoints para cada entidade:

### Base URL
```
http://localhost:3000/api
```

### Autenticação
- `POST /auth/login`: Autentica um usuário.
- `POST /auth/register`: Registra um novo usuário.

### Pacientes
- `GET /pacientes`: Lista todos os pacientes (com paginação).
- `GET /pacientes/:id`: Obtém detalhes de um paciente.
- `POST /pacientes`: Cria um novo paciente.
- `PUT /pacientes/:id`: Atualiza um paciente existente.
- `PATCH /pacientes/:id`: Atualiza parcialmente um paciente.
- `DELETE /pacientes/:id`: Exclui um paciente.

### Médicos
- `GET /medicos`: Lista todos os médicos.
- `GET /medicos/:id`: Obtém detalhes de um médico.
- `POST /medicos`: Cria um novo médico.
- `PUT /medicos/:id`: Atualiza um médico.
- `PATCH /medicos/:id`: Atualiza parcialmente um médico.
- `DELETE /medicos/:id`: Exclui um médico.

### Consultas
- `GET /consultas`: Lista todas as consultas (filtros: ?id_paciente=1, ?id_medico=2, ?data_inicio=2025-06-01).
- `GET /consultas/:id`: Obtém detalhes de uma consulta.
- `POST /consultas`: Cria uma nova consulta.
- `PUT /consultas/:id`: Atualiza uma consulta.
- `PATCH /consultas/:id`: Atualiza parcialmente uma consulta.
- `DELETE /consultas/:id`: Cancela uma consulta.

### Prontuários
- `GET /prontuarios`: Lista prontuários (filtro: ?id_paciente=1).
- `GET /prontuarios/:id`: Obtém um prontuário.
- `POST /prontuarios`: Cria um novo prontuário.
- `PUT /prontuarios/:id`: Atualiza um prontuário.
- `DELETE /prontuarios/:id`: Exclui um prontuário.

### Exames
- `GET /exames`: Lista exames (filtros: ?id_paciente=1, ?id_consulta=1).
- `GET /exames/:id`: Obtém detalhes de um exame.
- `POST /exames`: Cria um novo exame.
- `PUT /exames/:id`: Atualiza um exame.
- `PATCH /exames/:id`: Atualiza parcialmente um exame.
- `DELETE /exames/:id`: Exclui um exame.

### Prescrições
- `GET /prescricoes`: Lista prescrições (filtros: ?id_paciente=1, ?id_consulta=1).
- `GET /prescricoes/:id`: Obtém detalhes de uma prescrição.
- `POST /prescricoes`: Cria uma nova prescrição.
- `PUT /prescricoes/:id`: Atualiza uma prescrição.
- `PATCH /prescricoes/:id`: Atualiza parcialmente uma prescrição.
- `DELETE /prescricoes/:id`: Exclui uma prescrição.

## Autenticação e Autorização

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

### Exemplo de Uso
```javascript
// Login
fetch(\'http://localhost:3000/api/auth/login\', { method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    email: 'admin@clinica.com',
    senha: 'admin123'
  })
})
.then(response => response.json())
.then(data => {
  // Armazenar o token
  localStorage.setItem('token', data.data.token);
});

// Requisição autenticadfetch(\'http://localhost:3000/api/pacientes\', {
  headers: {
    'Authorization': `Bearer ${localStorage.getItem('token')}`
  }
})
.then(response => response.json())
.then(data => console.log(data));
```


## Testes

O projeto inclui testes automatizados para garantir a qualidade e o funcionamento correto da API e do frontend.

### Testes de Backend

Os testes de backend são implementados usando Jest e Supertest, e estão localizados no diretório `src/tests/`.

#### Estrutura dos Testes

- **api.test.js**: Testes básicos da API, verificando se os endpoints estão funcionando corretamente.
- **auth.test.js**: Testes de autenticação e autorização.
- **crud.test.js**: Testes de operações CRUD para cada entidade.
- **setup.js**: Configurações globais para os testes.

#### Executando os Testes

Para executar todos os testes:

```bash
cd clinica-api
npm test
```

Para executar um arquivo de teste específico:

```bash
npm test -- src/tests/api.test.js
```

#### Exemplos de Testes

##### Teste de Autenticação

```javascript
// src/tests/auth.test.js
describe('Autenticação', () => {
  it('deve registrar um novo usuário', async () => {
    const novoUsuario = {
      nome: 'Usuário Teste',
      email: 'usuario.teste@clinica.com',
      senha: 'senha123',
      role: 'recepcionista'
    };

    const response = await request(app)
      .post('/api/v1/auth/register')
      .send(novoUsuario);

    expect(response.status).toBe(201);
    expect(response.body).toHaveProperty('data');
    expect(response.body.data).toHaveProperty('usuario');
    expect(response.body.data).toHaveProperty('token');
    expect(response.body.data.usuario.email).toBe(novoUsuario.email);
  });

  it('deve fazer login como administrador', async () => {
    const credenciais = {
      email: 'admin@clinica.com',
      senha: 'admin123'
    };

    const response = await request(app)
      .post('/api/v1/auth/login')
      .send(credenciais);

    expect(response.status).toBe(200);
    expect(response.body).toHaveProperty('data');
    expect(response.body.data).toHaveProperty('usuario');
    expect(response.body.data).toHaveProperty('token');
    expect(response.body.data.usuario.role).toBe('admin');
  });
});
```

##### Teste de CRUD

```javascript
// src/tests/crud.test.js
describe('CRUD de Pacientes', () => {
  it('deve criar um novo paciente', async () => {
    const novoPaciente = {
      nome: 'Paciente Teste',
      cpf: '111.222.333-44',
      data_nascimento: '1990-01-01',
      telefone: '(11) 98765-4321',
      email: 'paciente.teste@email.com',
      endereco: 'Rua Teste, 123'
    };

    const response = await request(app)
      .post('/api/v1/pacientes')
      .set('Authorization', `Bearer ${token}`)
      .send(novoPaciente);

    expect(response.status).toBe(201);
    expect(response.body).toHaveProperty('data');
    expect(response.body.data).toHaveProperty('id_paciente');
  });

  it('deve atualizar um paciente existente', async () => {
    const dadosAtualizados = {
      nome: 'Paciente Teste Atualizado',
      cpf: '111.222.333-44',
      data_nascimento: '1990-01-01',
      telefone: '(11) 98765-4321',
      email: 'paciente.atualizado@email.com',
      endereco: 'Rua Teste Atualizada, 456'
    };

    const response = await request(app)
      .put(`/api/v1/pacientes/${pacienteId}`)
      .set('Authorization', `Bearer ${token}`)
      .send(dadosAtualizados);

    expect(response.status).toBe(200);
    expect(response.body).toHaveProperty('data');
    expect(response.body.data.nome).toBe(dadosAtualizados.nome);
    expect(response.body.data.email).toBe(dadosAtualizados.email);
  });
});
```

### Testes de Frontend

Os testes de frontend são manuais e podem ser realizados através da interface de usuário. O frontend foi desenvolvido para interagir com a API e testar todas as funcionalidades disponíveis.

#### Testando o Login

1. Acesse a página de login: `http://localhost:5173/login`
2. Utilize uma das seguintes credenciais:
   - Admin: admin@clinica.com / admin123
   - Médico: carlos@clinica.com / medico123
   - Recepcionista: maria@clinica.com / recep123
3. Verifique se o login é bem-sucedido e se você é redirecionado para o dashboard.

#### Testando o CRUD de Pacientes

1. Faça login no sistema.
2. Navegue até a página de pacientes: `http://localhost:5173/pacientes`
3. Teste as seguintes operações:
   - **Listar**: Verifique se a lista de pacientes é exibida corretamente.
   - **Criar**: Clique no botão "Novo Paciente", preencha o formulário e salve.
   - **Visualizar**: Clique em um paciente da lista para ver seus detalhes.
   - **Editar**: Clique no botão de edição, altere os dados e salve.
   - **Excluir**: Clique no botão de exclusão e confirme a operação.

#### Testando o CRUD de Consultas

1. Faça login no sistema.
2. Navegue até a página de consultas: `http://localhost:5173/consultas`
3. Teste as seguintes operações:
   - **Listar**: Verifique se a lista de consultas é exibida corretamente.
   - **Criar**: Clique no botão "Nova Consulta", preencha o formulário e salve.
   - **Visualizar**: Clique em uma consulta da lista para ver seus detalhes.
   - **Editar**: Clique no botão de edição, altere os dados e salve.
   - **Excluir**: Clique no botão de exclusão e confirme a operação.

#### Testando Permissões de Usuário

1. Faça login como recepcionista.
2. Verifique se você tem acesso apenas às páginas de pacientes, médicos e consultas.
3. Tente acessar uma página restrita, como prontuários: `http://localhost:5173/prontuarios`
4. Verifique se você é redirecionado ou se recebe uma mensagem de erro.
5. Repita o processo com diferentes tipos de usuário para verificar as permissões.

## Frontend

O frontend foi desenvolvido utilizando React e oferece uma interface amigável para interagir com a API. Ele inclui as seguintes funcionalidades:

- **Autenticação**: Login e registro de usuários.
- **Dashboard**: Visão geral do sistema com estatísticas e acesso rápido às principais funcionalidades.
- **Gerenciamento de Pacientes**: CRUD completo de pacientes.
- **Gerenciamento de Médicos**: CRUD completo de médicos.
- **Gerenciamento de Consultas**: CRUD completo de consultas.
- **Gerenciamento de Prontuários**: CRUD completo de prontuários (apenas para médicos e administradores).
- **Gerenciamento de Exames**: CRUD completo de exames (apenas para médicos e administradores).
- **Gerenciamento de Prescrições**: CRUD completo de prescrições (apenas para médicos e administradores).

### Tecnologias Utilizadas

- **React**: Biblioteca JavaScript para construção de interfaces de usuário.
- **React Router**: Para gerenciamento de rotas.
- **Axios**: Para requisições HTTP.
- **React Hook Form**: Para gerenciamento de formulários.
- **React Toastify**: Para notificações.
- **Tailwind CSS**: Para estilização.
- **Lucide React**: Para ícones.

### Estrutura de Arquivos

- **components/**: Componentes reutilizáveis.
- **pages/**: Páginas da aplicação.
- **services/**: Serviços para comunicação com a API.
- **App.jsx**: Componente principal da aplicação.
- **App.css**: Estilos globais.
- **main.jsx**: Ponto de entrada da aplicação.

## Executando o Projeto

### Backend

1. Inicie o servidor:
   ```bash
   cd clinica-api
   npm run dev
   ```
   O servidor estará disponível em `http://localhost:3000`.

### Frontend

1. Inicie o servidor de desenvolvimento:
   ```bash
   cd clinica-frontend
   npm run dev
   ```
   O frontend estará disponível em `http://localhost:5173`.

## Considerações de Segurança

O projeto implementa várias medidas de segurança:

1. **Autenticação com JWT**: Tokens JWT são utilizados para autenticar usuários.
2. **Controle de Acesso Baseado em Papéis (RBAC)**: Diferentes níveis de acesso são definidos para diferentes tipos de usuário.
3. **Validação de Dados**: Todos os dados de entrada são validados antes de serem processados.
4. **Proteção contra CSRF**: Tokens são utilizados para proteger contra ataques CSRF.
5. **Proteção contra SQL Injection**: O ORM Sequelize é utilizado para prevenir ataques de SQL Injection.
6. **Senhas Criptografadas**: As senhas são armazenadas de forma criptografada utilizando bcrypt.

## Melhorias Futuras

Algumas melhorias que podem ser implementadas no futuro:

1. **Testes Automatizados para o Frontend**: Implementar testes automatizados para o frontend utilizando Jest e React Testing Library.
2. **Implementação de WebSockets**: Para notificações em tempo real.
3. **Melhorias na Interface do Usuário**: Adicionar mais recursos visuais e melhorar a experiência do usuário.
4. **Implementação de Relatórios**: Adicionar funcionalidades para geração de relatórios.
5. **Integração com Serviços de Email**: Para envio de notificações por email.
6. **Implementação de PWA**: Transformar o frontend em um Progressive Web App.
7. **Melhorias na Segurança**: Implementar autenticação de dois fatores e outras medidas de segurança adicionais.

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

## Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

---

Desenvolvido por [Seu Nome] para o projeto de faculdade.

