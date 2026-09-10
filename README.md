# CineClube — Plataforma de Clubes de Cinema

Projeto integrador focado no desenvolvimento de uma aplicação full-stack para criação e gerenciamento de clubes de cinema entre amigos, permitindo a indicação de obras, acompanhamento de sessões e cálculo de notas médias por clube.

---

## 1. Status do Projeto

> **Fase Atual:** Fase 2 (Prototipagem, Definição de Arquitetura e Entrega Parcial).  
> **Backend:** Estrutura base gerada com Spring Boot 3 na porta `8080`.  
> **Frontend:** Estrutura de pastas inicializada.  
> **Banco de Dados:** Modelagem relacional definida; entidades e persistência em andamento.  
> **Controle de Versão:** Repositório configurado e sincronizado no GitLab.

---

## 2. Escopo da Aplicação (MVP)

A aplicação resolve a organização de listas de filmes compartilhadas entre círculos de amigos com as seguintes etapas:

* **Cadastro / Identificação:** Criação de perfil simples com nome, e-mail e `@usuario`.
* **Criação de Clube:** O usuário cria um espaço temático e atua como anfitrião.
* **Convite por `@usuario`:** Adição direta de membros conhecidos ao clube.
* **Catálogo do Clube:** Membros ativos adicionam títulos à lista do clube.
* **Avaliação Coletiva:** Membros atribuem notas (1 a 5) aos filmes assistidos, gerando a média daquele grupo.

---

## 3. Definição de Arquitetura

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
```

---

## 4. Prototipagem e Contratos da API (REST)

| Método | Endpoint | Descrição | Status Sucesso | Status Erro |
| :--- | :--- | :--- | :--- | :--- |
| `POST` | `/api/v1/usuarios` | Cadastro de perfil e identificador `@usuario` | `201 Created` | `400 Bad Request` |
| `POST` | `/api/v1/clubes` | Criação de clube de cinema | `201 Created` | `400 Bad Request` |
| `POST` | `/api/v1/clubes/{id}/membros` | Adição de membro ao clube por `@usuario` | `200 OK` | `404 Not Found` |
| `POST` | `/api/v1/clubes/{id}/filmes` | Adição de título à lista de exibição do clube | `201 Created` | `400 Bad Request` |
| `POST` | `/api/v1/filmes/{id}/avaliacoes` | Registro de nota (1 a 5) e atualização da média | `201 Created` | `400 Bad Request` |

### Regras de Negócio Críticas (Validações no Service)
* **RN01 (Acesso Restrito):** Apenas membros confirmados do clube podem sugerir títulos e emitir avaliações. Requisições externas são rejeitadas com erro `400`.
* **RN02 (Unicidade de Nota):** Cada membro pode avaliar uma única vez cada filme listado no clube.
* **RN03 (Integridade):** Validação de formato obrigatório para `@usuario` e restrição das notas ao intervalo de 1 a 5.

---

## 5. Instruções de Execução e Testes

### Configuração do Repositório Local
Para clonar e sincronizar com o GitLab:
```bash
git clone <URL_DO_REPOSITORIO_GITLAB>
cd cineclube-app
```

### Executando o Backend
Na pasta `backend`:
```bash
# Windows
.\mvnw.cmd spring-boot:run

# Linux / macOS
./mvnw spring-boot:run
```
O servidor estará acessível em `http://localhost:8080`.

### Executando os Testes Automatizados (Entrega Parcial)
Para validar os testes unitários e de contexto com JUnit:
```bash
# Windows
.\mvnw.cmd test

# Linux / macOS
./mvnw test
```
