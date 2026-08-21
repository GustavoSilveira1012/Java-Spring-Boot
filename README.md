# 🛒 Loja de Produtos — API REST

API REST completa para gerenciamento de uma loja de produtos, desenvolvida com **Java** e **Spring Boot**. O projeto implementa CRUD completo com relacionamento entre entidades, validações e tratamento de erros centralizado.

---

## 🚀 Tecnologias

![Java](https://img.shields.io/badge/Java-21-orange?style=flat-square&logo=java)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen?style=flat-square&logo=springboot)
![Spring Data JPA](https://img.shields.io/badge/Spring%20Data%20JPA-3.x-brightgreen?style=flat-square&logo=spring)
![H2 Database](https://img.shields.io/badge/H2-Database-blue?style=flat-square)
![Maven](https://img.shields.io/badge/Maven-Build-red?style=flat-square&logo=apachemaven)

---

## 📋 Funcionalidades

- ✅ CRUD completo de **Categorias**
- ✅ CRUD completo de **Produtos**
- ✅ Relacionamento entre entidades (`Categoria` → `Produto`)
- ✅ Validações de campos com Bean Validation
- ✅ Tratamento de erros centralizado com `@RestControllerAdvice`
- ✅ Busca de produtos por nome e por categoria
- ✅ Banco de dados H2 em memória (sem instalação)

---

## 🗂️ Estrutura do Projeto

```
src/main/java/com/loja/
├── controller/
│   ├── CategoriaController.java
│   └── ProdutoController.java
├── service/
│   ├── CategoriaService.java
│   └── ProdutoService.java
├── repository/
│   ├── CategoriaRepository.java
│   └── ProdutoRepository.java
├── model/
│   ├── Categoria.java
│   └── Produto.java
└── exception/
    ├── GlobalExceptionHandler.java
    └── ResourceNotFoundException.java
```

---

## 🔗 Relacionamento entre entidades

```
Categoria (1) ──────────── (N) Produto
   - id                          - id
   - nome                        - nome
   - descricao                   - preco
                                 - estoque
                                 - categoria_id (FK)
```

---

## 📡 Endpoints

### Categorias — `/categorias`

| Método | URL | Descrição |
|--------|-----|-----------|
| `GET` | `/categorias` | Lista todas as categorias |
| `GET` | `/categorias/{id}` | Busca categoria por ID |
| `POST` | `/categorias` | Cria nova categoria |
| `PUT` | `/categorias/{id}` | Atualiza categoria |
| `DELETE` | `/categorias/{id}` | Remove categoria |

### Produtos — `/produtos`

| Método | URL | Descrição |
|--------|-----|-----------|
| `GET` | `/produtos` | Lista todos os produtos |
| `GET` | `/produtos/{id}` | Busca produto por ID |
| `GET` | `/produtos/buscar?nome=X` | Busca produtos pelo nome |
| `GET` | `/produtos/categoria/{id}` | Lista produtos de uma categoria |
| `POST` | `/produtos` | Cria novo produto |
| `PUT` | `/produtos/{id}` | Atualiza produto |
| `DELETE` | `/produtos/{id}` | Remove produto |

---

## ▶️ Como rodar o projeto

### Pré-requisitos

- Java 21+
- Maven 3.8+

### Passos

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/loja-produtos-api.git

# Acesse a pasta
cd loja-produtos-api

# Rode o projeto
./mvnw spring-boot:run
```

A API estará disponível em: `http://localhost:8080`

Console do banco H2: `http://localhost:8080/h2-console`
> JDBC URL: `jdbc:h2:mem:loja` · Usuário: `sa` · Senha: *(vazio)*

---

## 🧪 Exemplos de uso

### Criar categoria

```http
POST /categorias
Content-Type: application/json

{
  "nome": "Eletrônicos",
  "descricao": "Smartphones, notebooks e acessórios"
}
```

**Resposta `201 Created`:**
```json
{
  "id": 1,
  "nome": "Eletrônicos",
  "descricao": "Smartphones, notebooks e acessórios"
}
```

---

### Criar produto

```http
POST /produtos
Content-Type: application/json

{
  "nome": "Notebook Dell",
  "preco": 4500.00,
  "estoque": 10,
  "categoria": { "id": 1 }
}
```

**Resposta `201 Created`:**
```json
{
  "id": 1,
  "nome": "Notebook Dell",
  "preco": 4500.00,
  "estoque": 10,
  "categoria": {
    "id": 1,
    "nome": "Eletrônicos"
  }
}
```

---

### Erros de validação

Campos inválidos retornam `400 Bad Request` com detalhes:

```json
{
  "preco": "O preço deve ser maior que zero",
  "nome": "O nome do produto é obrigatório"
}
```

Recurso não encontrado retorna `404 Not Found`:

```json
{
  "erro": "Produto não encontrado com id: 99"
}
```

---

## 📌 Decisões técnicas

- **H2 em memória** — facilita o desenvolvimento e testes sem configuração de banco externo. Para produção, basta trocar pela dependência do MySQL/PostgreSQL e ajustar o `application.properties`.
- **Bean Validation** — as validações ficam nas entidades (`@NotBlank`, `@Positive`, `@Min`), centralizadas e reutilizáveis.
- **`@RestControllerAdvice`** — tratamento de erros em um único lugar, evitando `try/catch` espalhado pelos controllers.
- **Camadas separadas** — Controller → Service → Repository, seguindo o padrão de responsabilidade única.

---

## 🛠️ Próximos passos

- [ ] Paginação e ordenação nos endpoints de listagem
- [ ] DTOs para desacoplar a camada de apresentação das entidades
- [ ] Autenticação com Spring Security + JWT
- [ ] Troca do H2 por MySQL/PostgreSQL
- [ ] Testes unitários com JUnit 5 e Mockito
- [ ] Deploy na Railway ou Render

---

## 👨‍💻 Autor

**Gustavo Silveira Soares**
Desenvolvedor Full Stack

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Gustavo%20Silveira-blue?style=flat-square&logo=linkedin)](https://linkedin.com/in/seu-perfil)
[![GitHub](https://img.shields.io/badge/GitHub-seu--usuario-black?style=flat-square&logo=github)](https://github.com/seu-usuario)
