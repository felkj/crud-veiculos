# Backend: Sistema de Gerenciamento de Veículos

## A Inteligência por Trás da Aplicação (Spring Boot)

Este `README.md` detalha o backend do nosso sistema de gerenciamento de veículos, construído com o **Spring Boot**. Ele funciona como uma API REST robusta e segura, pronta para atender a todas as requisições do seu frontend.

---

## 🔧 Estrutura do Projeto e Dependências

O projeto Spring Boot está montado com as peças essenciais para funcionar:

- **Web**: Para lidar com as requisições HTTP e as respostas REST.
- **JPA**: Para comunicação com o banco de dados.
- **Security (JWT)**: Para autenticação e autorização usando JSON Web Tokens.
- **Lombok**: Para deixar o código Java mais limpo.
- **Flyway**: Para migrações de banco de dados.
- **OpenAPI/Swagger**: Para documentação interativa da API.

---

## 1. 🗃️ Modelagem do Banco de Dados

A base sólida do sistema está no banco de dados **PostgreSQL**, com migrações gerenciadas pelo **Flyway**.

### 🧑‍💻 `users` — Gerenciando Usuários

| Campo      | Descrição |
|------------|-----------|
| `id`       | Identificador único, auto-gerado. |
| `username` | Nome de usuário único. |
| `password` | Senha criptografada com BCRYPT. |
| `cargo`    | Papel do usuário no sistema (ADMIN, USER). |

> **Observação:** Inserções iniciais (como admin/user) são definidas via `V1__create_users_table.sql`.

---

### 🚗 `veiculo` — Onde os Carros Vivem

| Campo          | Descrição |
|----------------|-----------|
| `id`           | Identificador exclusivo. |
| `marca`        | Marca do veículo (ex: Honda, Toyota). |
| `modelo`       | Modelo do veículo. |
| `url_image`    | Link para imagem do carro (pode ser nulo). |
| `ano`          | Ano de fabricação. |
| `preco`        | Valor de venda. |
| `vendido`      | Indica se foi vendido (`TRUE` ou `FALSE`). |
| `data_cadastro`| Data/hora de cadastro (imutável). |
| `data_venda`   | Data/hora de venda (preenchida ao marcar como vendido). |

> Adições como `url_image` estão definidas em migrações como `V2__add_image_url_to_veiculo.sql`.

---

## 2. 🔐 Autenticação e Autorização (JWT + Roles)

Segurança é prioridade! Implementamos autenticação via **JWT** e controle de acesso com **roles** (ADMIN, USER).

### Principais Componentes

- **`UserRoles.java`**: Enum com papéis de usuário.
- **`User.java`**: Entidade de usuário e integração com Spring Security.
- **`UserRepository.java`**: Interface de acesso ao banco.
- **`CustomUserDetailsService.java`**: Carregamento de dados do usuário.
- **`JwtUtil.java`**: Geração e validação de tokens.
- **`AuthRequest`**: DTO com `username` e `password`.
- **`AuthResponse`**: DTO com `JWT` e roles retornado no login.
- **`AuthController.java`**: Rota `/auth/login` para autenticação.

### Filtros e Handlers

- **`JwtRequestFilter.java`**: Verifica e valida o token nas requisições.
- **`JwtAuthenticationEntryPoint.java`**: Retorna 401 se o usuário não estiver autenticado.
- **`CustomAccessDeniedHandler.java`**: Retorna 403 se o usuário estiver autenticado, mas sem permissão.

### Configuração

- **`SecurityConfig.java`**: Define regras de acesso por endpoint e integra o filtro JWT.

---

## 3. 🔄 CRUD de Veículos

A API REST implementa o padrão **CRUD** (Create, Read, Update, Delete) completo.

### Entidades e Serviços

- **`Veiculo.java`**: Modelo da entidade. Campo `dataCadastro` é imutável. `setVendido()` preenche `dataVenda` automaticamente.
- **`VeiculoRepository.java`**: Interface de repositório para veículos.
- **`VeiculoService.java`**: Lógica de negócios, atualiza campos permitidos e ignora os imutáveis.
- **`VeiculoController.java`**: Define endpoints REST. Usa `@PreAuthorize` para proteger operações por role.

---

## 🌐 Configuração CORS

A classe **`CorsConfig.java`** conecta seu frontend (Angular em `http://localhost:4200`) com o backend (Spring Boot em `http://localhost:8080`), permitindo:

- Quais origens podem acessar.
- Quais métodos HTTP são aceitos.
- Quais cabeçalhos podem ser usados.

---

## ✅ Requisitos

- Java 17+
- Spring Boot 3.x
- PostgreSQL
- Maven
- Frontend Angular (opcional, mas recomendado)

---

## 📦 Inicialização

1. Execute as migrações Flyway.
2. Inicie o backend com Spring Boot.
3. Acesse os endpoints com um client (ex: Postman) ou via Swagger.
4. Realize o login e utilize o JWT para autenticar requisições protegidas.

---

Feito com 💻 e ☕ por Felipe
