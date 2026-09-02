# 🐱 NekoStock

> **Sistema de gerenciamento de estoque para lojas**

O **NekoStock** é um sistema web desenvolvido para auxiliar no gerenciamento de estoque de uma loja, permitindo o controle de produtos, categorias, entradas e saídas de estoque e movimentações realizadas pelos funcionários.

O projeto utiliza uma arquitetura **Front-end + API REST + Back-end + Banco de Dados**, permitindo aplicar conceitos de desenvolvimento web, orientação a objetos, persistência de dados e organização em camadas.

---

## 🎯 Objetivo

O principal objetivo do NekoStock é facilitar o controle e acompanhamento do estoque, centralizando as informações dos produtos e suas movimentações em um único sistema.

O sistema busca reduzir erros de controle manual, facilitar a consulta de produtos e fornecer uma visão geral da situação do estoque.

---

## 🚀 Funcionalidades

### 🔐 Autenticação

- Login de funcionários;
- Validação de acesso;
- Controle de usuários.

### 📦 Produtos

- Cadastro de produtos;
- Edição de produtos;
- Exclusão de produtos;
- Consulta de produtos;
- Busca por nome;
- Filtro por categoria;
- Controle de quantidade em estoque.

### 📊 Estoque

- Registro de entrada de produtos;
- Registro de saída de produtos;
- Atualização automática da quantidade disponível;
- Identificação de produtos com estoque baixo;
- Identificação de produtos sem estoque.

### 📋 Histórico

- Registro das movimentações realizadas;
- Consulta de entradas e saídas;
- Informações sobre alterações no estoque.

### 📈 Dashboard

O sistema contará com um painel para apresentar informações gerais do estoque:

- **Total de produtos**
- **Produtos em estoque**
- **Produtos com estoque baixo**
- **Produtos sem estoque**

---

## 🛠️ Tecnologias

### Front-end

- HTML5
- CSS3
- JavaScript

Responsável pela interface e pelas interações realizadas pelo usuário.

### Back-end

- Java
- Spring Boot
- Spring Web
- Spring Data JPA
- Hibernate

Responsável pelas regras de negócio, processamento das requisições e disponibilização da API REST.

### Banco de dados

- MySQL

Responsável pelo armazenamento persistente das informações do sistema.

### Ferramentas

- Git
- GitHub
- IntelliJ IDEA / VS Code
- Maven

---

## 🏗️ Arquitetura

O NekoStock utiliza uma arquitetura dividida em camadas, buscando separar as responsabilidades de cada parte do sistema.

```text
┌─────────────────────────┐
│       FRONT-END         │
│    HTML / CSS / JS      │
└────────────┬────────────┘
             │
             │ HTTP / JSON
             ▼
┌─────────────────────────┐
│       API REST          │
│      Spring Boot        │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     CAMADA DE NEGÓCIO   │
│        Services         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│      PERSISTÊNCIA       │
│    JPA / Hibernate      │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│       BANCO DE DADOS    │
│          MySQL          │
└─────────────────────────┘
```

### Fluxo de uma requisição

```text
Usuário
   ↓
HTML / CSS / JavaScript
   ↓
Requisição HTTP
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
JPA / Hibernate
   ↓
MySQL
```

---

## 📂 Estrutura do projeto

```text
NekoStock/
│
├── frontend/
│   │
│   ├── index.html
│   ├── login.html
│   ├── produtos.html
│   ├── estoque.html
│   ├── style.css
│   └── script.js
│
├── backend/
│   │
│   ├── pom.xml
│   │
│   └── src/
│       └── main/
│           ├── java/
│           │   └── com/
│           │       └── nekostock/
│           │           │
│           │           ├── controller/
│           │           ├── service/
│           │           ├── model/
│           │           ├── repository/
│           │           │
│           │           └── NekoStockApplication.java
│           │
│           └── resources/
│               └── application.properties
│
├── docs/
│
└── README.md
```

---

## 🧩 Organização do Back-end

O back-end será organizado utilizando o padrão de separação por responsabilidades:

### `controller/`

Responsável por receber as requisições HTTP e disponibilizar os endpoints da API.

Exemplo:

```text
ProdutoController
EstoqueController
UsuarioController
```

### `service/`

Contém as regras de negócio da aplicação.

Exemplo:

```text
ProdutoService
EstoqueService
UsuarioService
```

### `model/`

Representa as entidades utilizadas pelo sistema.

Exemplo:

```text
Produto
Categoria
Usuario
MovimentacaoEstoque
```

### `repository/`

Responsável pela comunicação entre a aplicação e o banco de dados utilizando Spring Data JPA.

Exemplo:

```text
ProdutoRepository
CategoriaRepository
UsuarioRepository
MovimentacaoRepository
```

---

## 🗄️ Banco de dados

O banco de dados será responsável por armazenar as principais informações do sistema.

Estrutura inicial prevista:

```text
USUARIO
 ├── id
 ├── nome
 ├── email
 └── senha

CATEGORIA
 ├── id
 └── nome

PRODUTO
 ├── id
 ├── nome
 ├── descricao
 ├── preco
 ├── quantidade
 └── categoria_id

MOVIMENTACAO
 ├── id
 ├── tipo
 ├── quantidade
 ├── data
 ├── produto_id
 └── usuario_id
```

> A estrutura poderá ser modificada durante o desenvolvimento do projeto.

---

## 📌 Regras de negócio

Entre as regras previstas para o NekoStock estão:

1. Um produto não pode possuir cadastro duplicado.
2. Uma saída de estoque não pode ser realizada quando a quantidade solicitada for maior que a quantidade disponível.
3. Toda entrada ou saída deve gerar um registro no histórico.
4. A quantidade do produto deve ser atualizada após uma movimentação.
5. Produtos abaixo do limite mínimo definido devem ser identificados como **estoque baixo**.
6. Produtos com quantidade igual a zero devem ser identificados como **sem estoque**.
7. Operações restritas devem exigir autenticação do funcionário.

---

## ⚙️ Como executar o projeto

### Pré-requisitos

Antes de executar o projeto, instale:

- Java JDK
- Maven
- MySQL
- Git

### 1. Clonar o repositório

```bash
git clone URL_DO_REPOSITORIO
```

### 2. Entrar na pasta

```bash
cd NekoStock
```

### 3. Configurar o banco

Crie um banco de dados MySQL para o projeto e configure as informações de conexão no arquivo:

```text
backend/src/main/resources/application.properties
```

Exemplo:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/nekostock
spring.datasource.username=root
spring.datasource.password=SUA_SENHA

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

> Não coloque senhas reais no repositório público.

### 4. Executar o back-end

Entre na pasta:

```bash
cd backend
```

Execute:

```bash
mvn spring-boot:run
```

### 5. Executar o front-end

Abra os arquivos HTML do diretório `frontend/` utilizando um servidor local.

---

\<div align="center">

### 🐱 NekoStock

**Controle seu estoque. Simplifique seu negócio.**

\</div>
