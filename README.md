# CineClube — Plataforma de Clubes de Cinema

Projeto integrador focado no desenvolvimento de uma aplicação full-stack para criação e gerenciamento de clubes de cinema entre amigos, permitindo a indicação de obras, acompanhamento de sessões e cálculo de notas médias por clube.

---

## 1. Status do Projeto

> **Fase Atual:** Fase 1 / Início da Fase 2 (Estruturação de Ambiente, Repositório e Definição de Escopo).  
> **Backend:** Estrutura base gerada com Spring Boot 3 na porta `8080`.  
> **Frontend:** Estrutura de pastas inicializada.  
> **Banco de Dados:** Modelagem relacional definida; scripts e entidades em andamento.

---

## 2. Escopo da Aplicação (MVP)

A aplicação resolve a organização de listas de filmes compartilhadas entre círculos de amigos com as seguintes etapas:

* **Cadastro / Identificação:** Criação de perfil simples com nome, e-mail e `@usuario`.
* **Criação de Clube:** O usuário cria um espaço temático e atua como anfitrião.
* **Convite por `@usuario`:** Adição direta de membros conhecidos ao clube.
* **Catálogo do Clube:** Membros ativos adicionam títulos à lista do clube.
* **Avaliação Coletiva:** Membros atribuem notas (1 a 5) aos filmes assistidos, gerando a média daquele grupo.

---

## 3. Planejamento de Arquitetura

O sistema adota uma arquitetura em camadas desacoplada:

* **Frontend:** Interface desenvolvida em React.js (consumo via `fetch`/`axios`).
* **Backend:** API REST desenvolvida em Java com Spring Boot 3 e Maven.
* **Persistência:** PostgreSQL (mapeamento via Spring Data JPA / Hibernate).
* **Segurança de Negócio:** Validações de acesso e consistência centralizadas na camada de serviço (`Service`).

### Estrutura de Diretórios Planejada

```text
cineclube-app/
├── backend/          # API Spring Boot (Maven, Controllers, Services, Repositories)
├── frontend/         # Cliente React.js
├── docs/             # Diagramas e documentações auxiliares
└── README.md         # Acompanhamento do projeto
