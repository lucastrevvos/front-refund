# Refund Web

Interface web para solicitação, acompanhamento e consulta de reembolsos corporativos.

## Visão geral

Refund Web é uma aplicação front-end construída para organizar o fluxo de reembolsos entre colaboradores e gestores. A plataforma oferece uma experiência simples para registrar despesas com comprovantes e uma visão administrativa para consultar solicitações enviadas.

O projeto foi desenvolvido com foco em uma interface objetiva, autenticação por perfil de usuário e integração com uma API REST responsável por sessões, usuários, uploads e reembolsos.

## Problema

Processos de reembolso podem se tornar dispersos quando dependem de mensagens, planilhas ou envio manual de comprovantes. Esse cenário dificulta a padronização das solicitações, a consulta de histórico e a análise por parte de gestores ou áreas financeiras.

## Solução

A aplicação centraliza o fluxo de reembolso em uma interface web com dois caminhos principais:

- colaboradores autenticados registram uma solicitação com nome, categoria, valor e comprovante;
- gestores autenticados acessam uma lista paginada de solicitações, podem pesquisar por nome e abrir os detalhes de cada reembolso.

Com isso, o projeto organiza a jornada de envio e consulta em telas dedicadas, com validação de dados no front-end e comunicação com serviços externos via HTTP.

## Funcionalidades

- Cadastro de usuário.
- Autenticação de usuário com persistência de sessão em `localStorage`.
- Controle de rotas por perfil: `employee` e `manager`.
- Criação de solicitação de reembolso com categoria, valor e upload de comprovante.
- Validação de formulários com Zod.
- Tela de confirmação após envio da solicitação.
- Dashboard gerencial com listagem paginada de reembolsos.
- Pesquisa de solicitações por nome no dashboard.
- Visualização de detalhes de uma solicitação existente.
- Link para abertura do comprovante associado ao reembolso.
- Componentes reutilizáveis de formulário, botão, upload, paginação, layout e item de reembolso.

## Stack

- React 19
- TypeScript
- Vite
- React Router
- Tailwind CSS
- Axios
- Zod
- clsx
- tailwind-merge

## Arquitetura

A aplicação segue uma organização por responsabilidade, separando telas, rotas, componentes, contexto de autenticação, serviços HTTP, tipos de dados e utilitários.

```text
src/
├── assets/        # Ícones e imagens usados na interface
├── components/    # Componentes reutilizáveis de UI
├── contexts/      # Contexto global de autenticação
├── dtos/          # Tipagens de respostas e entidades da API
├── hooks/         # Hooks de acesso a contextos e comportamentos compartilhados
├── pages/         # Telas da aplicação
├── routes/        # Definição de rotas por perfil de usuário
├── services/      # Cliente HTTP para comunicação com a API
└── utils/         # Funções auxiliares e mapeamentos de domínio
```

O `AuthProvider` centraliza a sessão do usuário, salva token e dados básicos no navegador e configura o cabeçalho `Authorization` do Axios. As rotas são selecionadas dinamicamente de acordo com o perfil retornado pela autenticação, mantendo experiências distintas para colaboradores e gestores.

## Como rodar

### Pré-requisitos

- Node.js em versão compatível com Vite 6.
- npm.
- API de reembolsos disponível localmente para atender às rotas usadas pela aplicação.

### Passo a passo

1. Clone o repositório:

```bash
git clone <url-do-repositorio>
```

2. Acesse a pasta do projeto:

```bash
cd front-refund
```

3. Instale as dependências:

```bash
npm install
```

4. Inicie o servidor de desenvolvimento:

```bash
npm run dev
```

5. Acesse a aplicação no endereço exibido pelo Vite no terminal.

### Build de produção

```bash
npm run build
```

### Preview do build

```bash
npm run preview
```

## Configuração

A aplicação consome uma API REST configurada no cliente Axios.

Configuração utilizada em ambiente local:

```text
API base URL: http://localhost:3333
```

Endpoints consumidos pela interface:

- `POST /sessions`
- `POST /users`
- `POST /uploads`
- `POST /refunds`
- `GET /refunds`
- `GET /refunds/:id`
- `GET /uploads/:filename`

Este repositório não expõe tokens, chaves privadas ou credenciais. A autenticação é realizada por meio do token retornado pela API no fluxo de login.

## Decisões técnicas

- **React com TypeScript:** combinação usada para criar uma interface componentizada com tipagem estática nas principais estruturas da aplicação.
- **Vite:** escolhido para oferecer uma experiência de desenvolvimento rápida e um processo de build simples.
- **React Router:** utilizado para separar rotas públicas, rotas de colaborador e rotas de gestor.
- **Context API:** centraliza autenticação, sessão e logout sem adicionar uma biblioteca externa de estado global.
- **Axios:** encapsula a comunicação HTTP com a API e permite configurar o token de autenticação em um ponto único.
- **Zod:** valida os dados dos formulários antes do envio para a API, melhorando a consistência das entradas do usuário.
- **Tailwind CSS:** estrutura a estilização diretamente nos componentes, com tokens visuais definidos para cores, fonte e escala de texto.
- **Componentes reutilizáveis:** inputs, selects, botões, upload, paginação e layouts foram separados para manter a interface consistente e facilitar evolução.

## Status

O projeto apresenta um fluxo funcional de autenticação, cadastro, criação de reembolsos, upload de comprovantes e consulta gerencial. A aplicação está organizada como uma peça de portfólio front-end integrada a uma API REST local.

## Roadmap

- Adicionar feedback visual mais detalhado para estados de sucesso e erro.
- Evoluir filtros do dashboard com novas opções de busca e ordenação.
- Incluir tela de perfil do usuário autenticado.
- Adicionar testes automatizados para fluxos principais da interface.
- Preparar configuração flexível de ambiente para diferentes URLs de API.
- Publicar uma versão demonstrável com backend e front-end hospedados.

## O que este projeto demonstra

- Construção de SPA com React, TypeScript e Vite.
- Organização de rotas protegidas por autenticação e perfil de usuário.
- Integração com API REST usando Axios.
- Persistência de sessão no navegador.
- Validação de formulários com Zod.
- Upload de arquivos via `FormData`.
- Criação de componentes reutilizáveis e layouts consistentes.
- Aplicação de Tailwind CSS em uma interface responsiva.
- Separação clara entre páginas, serviços, contexto, rotas, componentes e utilitários.
