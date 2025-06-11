# 🚗 Sistema de Gerenciamento de Veículos

## Uma Jornada de Desenvolvimento: Do Banco de Dados ao Frontend Moderno

Bem-vindo(a) ao repositório do **Sistema de Gerenciamento de Veículos**!  
Este projeto foi desenvolvido passo a passo, unindo a robustez do **Spring Boot** no backend com a interatividade do **Angular 19** no frontend.

Nosso objetivo? Criar uma aplicação **segura**, **eficiente** e **intuitiva** para o gerenciamento completo de veículos: cadastrar, listar, editar, excluir — tudo isso com controle de acesso por **papéis de usuário (roles)**.

---

## 🗄️ 1. Modelagem do Banco de Dados: O Coração da Aplicação

### Banco de Dados: PostgreSQL + Flyway
A fundação do sistema é um banco **PostgreSQL**, com versionamento e migrações gerenciadas pelo **Flyway**.
Lembre-se de subir o docker-compose.yml para subir o banco e assim rodar o projeto.

### Tabela: `users` - Gerenciando Acesso
| Campo      | Descrição |
|------------|-----------|
| `id`       | Identificador único (auto gerado) |
| `username` | Nome de usuário único |
| `password` | Hash seguro BCRYPT |
| `cargo`    | Papel (ADMIN / USER) |

📁 Migração: `V1__create_users_table.sql`  
Contém criação e inserção de usuários iniciais com senhas criptografadas.

### Tabela: `veiculo` - Onde os Carros Vivem
| Campo          | Descrição |
|----------------|-----------|
| `id`           | ID exclusivo (auto gerado) |
| `marca`        | Marca do carro (ex: Honda) |
| `modelo`       | Modelo (ex: Civic) |
| `url_image`    | Link para imagem (opcional) |
| `ano`          | Ano de fabricação |
| `preco`        | Valor de venda |
| `vendido`      | TRUE/FALSE |
| `data_cadastro`| Data de inserção (imutável) |
| `data_venda`   | Data em que foi vendido |

📁 Migração: `V2__add_image_url_to_veiculo.sql`  
Adiciona a coluna `url_image`.

---

## 💻 2. Backend: Inteligência da Aplicação (Spring Boot)

### Tecnologias e Dependências
- `spring-boot-starter-web`
- `spring-boot-starter-security`
- `spring-boot-starter-data-jpa`
- `jjwt` (JSON Web Token)
- `Lombok`
- `Flyway`

### Segurança com JWT + Roles
- **UserRoles.java**: Enum com os papéis disponíveis (ADMIN, USER)
- **User.java**: Entidade de usuário com compatibilidade ao Spring Security
- **UserRepository.java**: Interface de persistência dos usuários
- **CustomUserDetailsService.java**: Serviço que carrega o usuário no login
- **JwtUtil.java**: Criação e verificação de tokens JWT
- **AuthRequest/AuthResponse.java**: DTOs de autenticação
- **AuthController.java**: Endpoint `/auth/login`
- **JwtRequestFilter.java**: Filtro de autenticação nas requisições
- **JwtAuthenticationEntryPoint.java**: Retorno 401 personalizado
- **CustomAccessDeniedHandler.java**: Retorno 403 personalizado
- **SecurityConfig.java**: Define permissões por endpoint

### CRUD de Veículos
- **Veiculo.java**: Entidade com lógica para atualizar `dataVenda`
- **VeiculoRepository.java**: Interface para operações básicas
- **VeiculoService.java**: Regra de negócio com atualização seletiva
- **VeiculoController.java**: REST API com endpoints protegidos via `@PreAuthorize`

### 🌐 CORS
- Configuração no `CorsConfig.java` para permitir integração entre `localhost:4200` e `localhost:8080`

---

## 🎨 3. Frontend: A Experiência do Usuário (Angular 19)

### Tecnologias Utilizadas
- **Angular 19 Standalone**
- **Bootstrap 5**
- **Bootstrap Icons**

### Estrutura do Projeto (Angular)
- Totalmente baseado em **Standalone Components** para organização e performance.
- Estilização moderna com Bootstrap.

---

## ✅ Conclusão

Este projeto integra boas práticas modernas de desenvolvimento web full-stack, oferecendo uma aplicação real para gestão de veículos. Desde a modelagem do banco até o consumo da API em um frontend moderno, este sistema é um ótimo exemplo de integração entre backend e frontend.

---

### 🚀 Pronto para usar?
Clone o repositório, configure as variáveis de ambiente e aproveite!

```bash
git clone https://github.com/felkj/crud-veiculos.git
```

---

Feito por Felipe.
