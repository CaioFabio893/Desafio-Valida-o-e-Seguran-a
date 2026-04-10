# 🔐 Desafio Validação e Segurança — Spring Boot + OAuth2

API RESTful desenvolvida com foco em **segurança**, **validação de dados** e **controle de acesso por perfis de usuário**, utilizando Java, Spring Boot, Spring Security e OAuth2.

---

## 📋 Sobre o Projeto

Sistema de gerenciamento de **Eventos e Cidades** com relação N-1 entre as entidades, construído sob a metodologia **TDD (Test-Driven Development)**. O projeto foi desenvolvido como desafio prático do curso **Java Spring Professional** da [DevSuperior](https://devsuperior.com.br), com avaliação automatizada via coleção Postman.

**Resultado:** ✅ 12/12 critérios aprovados

---

## 🏗️ Modelo de Domínio

```
City (1) ───── (N) Event
```

- Uma **Cidade** pode ter vários **Eventos**
- Um **Evento** pertence a exatamente uma **Cidade**

---

## 🔒 Regras de Controle de Acesso

| Operação          | Público | CLIENT | ADMIN |
|-------------------|:-------:|:------:|:-----:|
| GET /events       | ✅      | ✅     | ✅    |
| POST /events      | ❌      | ✅     | ✅    |
| GET /cities       | ✅      | ✅     | ✅    |
| POST /cities      | ❌      | ❌     | ✅    |

---

## ✅ Regras de Validação

**City:**
- `name` — não pode ser vazio

**Event:**
- `name` — não pode ser vazio
- `date` — não pode ser uma data no passado
- `city` — não pode ser nula

---

## 🧪 Critérios de Avaliação (12/12)

| # | Critério | Status |
|---|----------|--------|
| 1 | `POST /events` retorna **401** para usuário não autenticado | ✅ |
| 2 | `POST /events` retorna **201** para CLIENT com dados válidos | ✅ |
| 3 | `POST /events` retorna **201** para ADMIN com dados válidos | ✅ |
| 4 | `POST /events` retorna **422** para ADMIN com nome em branco | ✅ |
| 5 | `POST /events` retorna **422** para ADMIN com data no passado | ✅ |
| 6 | `POST /events` retorna **422** para ADMIN com cidade nula | ✅ |
| 7 | `GET /events` retorna **200** com página de recursos | ✅ |
| 8 | `POST /cities` retorna **401** para usuário não autenticado | ✅ |
| 9 | `POST /cities` retorna **403** para CLIENT autenticado | ✅ |
| 10 | `POST /cities` retorna **201** para ADMIN com dados válidos | ✅ |
| 11 | `POST /cities` retorna **422** para ADMIN com nome em branco | ✅ |
| 12 | `GET /cities` retorna **200** com recursos ordenados por nome | ✅ |

---

## 🛠️ Tecnologias Utilizadas

- **Java 17**
- **Spring Boot 3**
- **Spring Security** — autenticação e autorização
- **OAuth2 / JWT** — tokens de acesso
- **Spring Data JPA** — persistência
- **Bean Validation** — validação de dados (`@NotBlank`, `@Future`, `@NotNull`)
- **H2 Database** — banco em memória para testes
- **Maven** — gerenciamento de dependências
- **Postman** — coleção de testes automatizados

---

## 🚀 Como Executar

### Pré-requisitos
- Java 17+
- Maven 3.8+

### Passos

```bash
# Clone o repositório
git clone https://github.com/CaioFabio893/Desafio-Valida-o-e-Seguran-a.git

# Entre na pasta do projeto
cd Desafio-Valida-o-e-Seguran-a

# Execute a aplicação
./mvnw spring-boot:run
```

A API estará disponível em: `http://localhost:8080`

---

## 🔑 Autenticação

A API utiliza **OAuth2 com JWT**. Para obter um token:

```http
POST /oauth2/token
Content-Type: application/x-www-form-urlencoded

grant_type=password&username={email}&password={senha}&client_id=myclientid&client_secret=myclientsecret
```

Utilize o token retornado no header `Authorization: Bearer {token}` nas requisições protegidas.

### Usuários de teste (seed)

| Perfil | Email | Senha |
|--------|-------|-------|
| ADMIN  | alex@gmail.com | 123456 |
| CLIENT | maria@gmail.com | 123456 |

---

## 📁 Estrutura do Projeto

```
src/
├── main/
│   ├── java/
│   │   └── com/devsuperior/demo/
│   │       ├── config/         # Configurações de segurança e OAuth2
│   │       ├── controllers/    # Endpoints REST (CityController, EventController)
│   │       ├── dto/            # Data Transfer Objects com validações
│   │       ├── entities/       # Entidades JPA (City, Event)
│   │       ├── repositories/   # Repositórios Spring Data
│   │       └── services/       # Regras de negócio
│   └── resources/
│       ├── application.properties
│       └── import.sql          # Dados iniciais
└── test/
    └── java/                   # Testes de integração
```

---

## 📌 Competências Demonstradas

- Desenvolvimento **TDD** de API REST com Java e Spring Boot
- Implementação de segurança com **Spring Security e OAuth2**
- **Controle de acesso por rotas e perfis** de usuário (ROLE_CLIENT, ROLE_ADMIN)
- **Validação de dados** com Bean Validation e tratamento de erros padronizado (RFC 7807)
- Boas práticas de design de API REST (status codes corretos, respostas paginadas)

---

## 📄 Licença

Este projeto foi desenvolvido para fins educacionais como parte do curso **Java Spring Professional — DevSuperior**.
