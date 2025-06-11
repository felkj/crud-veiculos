
# Frontend: Sistema de Gerenciamento de Veículos

## A Experiência do Usuário (Angular 19 Standalone)

Este README.md é dedicado ao frontend do seu sistema de gerenciamento de veículos. Ele é a parte visível da aplicação, desenvolvida com a versão mais recente do Angular (Angular 19), utilizando o conceito moderno de Standalone Components. Isso torna o código mais organizado e fácil de manter. Para deixar tudo bonito e funcional, usamos Bootstrap para estilização e Bootstrap Icons para os ícones.

---

## Estrutura do Projeto e Dependências

O projeto Angular está configurado para ser totalmente standalone. As principais "ferramentas" que ele usa estão listadas no arquivo `package.json`:

- As bibliotecas centrais do Angular (`@angular/core`, `@angular/common`, `@angular/router`, `@angular/forms`, `@angular/platform-browser`).
- `bootstrap` e `bootstrap-icons`: Para dar o visual elegante e os ícones à sua aplicação.
- `jwt-decode`: Uma pequena biblioteca que nos ajuda a "ler" as informações dentro do JWT no lado do frontend, como a data de expiração e os papéis.

Você pode verificar essas dependências no seu `package.json`.

---

## Configuração Geral do Angular

- `main.ts`: Este é o ponto de partida da sua aplicação Angular. Ele inicializa tudo, "acordando" o componente principal (`AppComponent`) e carregando as configurações globais do `app.config.ts`.
- `app.config.ts`: É o local onde configuramos os "serviços" que estarão disponíveis para toda a sua aplicação. Aqui, habilitamos o `HttpClient` (para fazer requisições HTTP), registramos o `AuthInterceptor` (que vai adicionar o token JWT nas requisições), e configuramos o `LOCALE_ID` para `pt-BR`.
- `app.routes.ts`: Define todas as rotas da aplicação. Usamos `AuthGuard` para proteger as rotas conforme a autenticação e o papel do usuário.
- `angular.json`: Este arquivo garante que Bootstrap (CSS e JavaScript) e Bootstrap Icons sejam carregados globalmente em seu projeto.

---

## Autenticação e Autorização (Frontend)

- **AuthService**: Lida com login, logout, e fornece métodos como `isAuthenticated()` e `hasRole()`. Implementado em `auth.service.ts`.
- **AuthInterceptor**: Intercepta todas as requisições HTTP e injeta o token JWT se disponível. Implementado em `auth.interceptor.ts`.
- **AuthGuard**: Protege rotas de acordo com autenticação e papel. Implementado em `auth.guard.ts`.

---

## Componentes CRUD de Veículos

- **LoginComponent**: Apresenta o formulário de login e exibe mensagens em caso de erro.
- **LayoutComponent**: Contém o `HeaderComponent`, `<router-outlet>` e `FooterComponent`.
- **HeaderComponent**: Mostra links com base no papel do usuário e o botão de logout.
- **FooterComponent**: Contém informações adicionais, como contatos.
- **CadastroComponent**: Permite adicionar novos veículos. Visível apenas para ADMIN.
- **ListarComponent**: Lista os veículos e permite editar/excluir (ADMIN). Utiliza diálogo de confirmação para exclusão.
- **EditarComponent**: Permite editar os detalhes de um veículo com base no ID da URL. Apenas para ADMIN.

---

## Estilização (CSS)

A beleza da aplicação vem do uso do Bootstrap e de CSS customizado por componente (`*.component.css`). O layout é responsivo, e elementos como imagens e modais foram estilizados com atenção ao detalhe para boa experiência em todas as telas.
