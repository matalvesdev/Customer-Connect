# Customer Connect 🚀

API RESTful para gerenciamento de clientes desenvolvida com Spring Boot e MySQL.

## 📋 Sobre o Projeto

Customer Connect é uma aplicação backend robusta para gerenciar cadastros de clientes, oferecendo operações CRUD completas com recursos de paginação, ordenação e filtros personalizados.

## ✨ Funcionalidades

- ✅ **Criar** novos clientes
- 🔍 **Listar** clientes com paginação e filtros
- 👤 **Buscar** cliente por ID
- ✏️ **Atualizar** informações de clientes
- 🗑️ **Deletar** clientes
- 🔎 **Filtrar** por CPF e/ou Email
- 📄 **Paginação** e ordenação customizáveis

## 🛠️ Tecnologias Utilizadas

- **Java 21** - Linguagem de programação
- **Spring Boot 3.5.0** - Framework principal
- **Spring Data JPA** - Persistência de dados
- **MySQL 8.x** - Banco de dados relacional
- **Maven** - Gerenciador de dependências
- **Docker** - Containerização do banco de dados
- **Hibernate** - ORM (Object-Relational Mapping)

## 📦 Estrutura do Projeto

```
Customer-Connect/
├── src/
│   └── main/
│       ├── java/
│       │   └── matalvesdev/
│       │       └── CustomerConnect/
│       │           ├── controller/
│       │           │   ├── dto/
│       │           │   └── CustomerController.java
│       │           ├── entity/
│       │           │   └── CustomerEntity.java
│       │           ├── repository/
│       │           │   └── CustomerRepository.java
│       │           ├── service/
│       │           │   └── CustomerService.java
│       │           └── CustomerConnectApplication.java
│       └── resources/
│           └── application.properties
├── docker/
│   └── docker-compose.yml
├── pom.xml
└── README. md
```

## 🗄️ Modelo de Dados

### CustomerEntity

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `customerId` | Long | ID único (gerado automaticamente) |
| `name` | String | Nome do cliente |
| `cpf` | String | CPF (único) |
| `email` | String | Email (único) |
| `phoneNumber` | String | Número de telefone |
| `createdAt` | LocalDateTime | Data de criação (automática) |
| `updatedAt` | LocalDateTime | Data de atualização (automática) |

## 🚀 Como Executar

### Pré-requisitos

- Java 21 ou superior
- Maven 3.6+
- Docker e Docker Compose

### Passo 1: Clone o repositório

```bash
git clone https://github.com/matalvesdev/Customer-Connect.git
cd Customer-Connect
```

### Passo 2: Inicie o banco de dados MySQL com Docker

```bash
cd docker
docker-compose up -d
```

Isso irá criar um container MySQL com as seguintes configurações:
- **Database**: mydatabase
- **User**: user
- **Password**: 123
- **Port**: 3306

### Passo 3: Execute a aplicação

```bash
# Volte para o diretório raiz
cd ..

# Execute com Maven
./mvnw spring-boot:run

# Ou compile e execute o JAR
./mvnw clean package
java -jar target/CustomerConnect-0.0.1-SNAPSHOT. jar
```

A aplicação estará disponível em:  `http://localhost:8080`

## 📡 API Endpoints

### Criar Cliente
```http
POST /customers
Content-Type: application/json

{
  "name": "João Silva",
  "cpf": "12345678900",
  "email": "joao@example.com",
  "phoneNumber": "(11) 98765-4321"
}
```

**Resposta**:  `201 Created` com header `Location: /customers/{id}`

### Listar Clientes (com paginação e filtros)
```http
GET /customers?page=0&pageSize=10&orderBy=desc&cpf=12345678900&email=joao@example. com
```

**Parâmetros de Query**:
- `page` (opcional, padrão: 0) - Número da página
- `pageSize` (opcional, padrão: 10) - Tamanho da página
- `orderBy` (opcional, padrão: desc) - Ordenação (asc/desc)
- `cpf` (opcional) - Filtro por CPF
- `email` (opcional) - Filtro por Email

**Resposta**: `200 OK`
```json
{
  "data": [... ],
  "pagination": {
    "page": 0,
    "pageSize": 10,
    "totalElements": 100,
    "totalPages": 10
  }
}
```

### Buscar Cliente por ID
```http
GET /customers/{customerId}
```

**Resposta**: `200 OK` ou `404 Not Found`

### Atualizar Cliente
```http
PUT /customers/{customerId}
Content-Type: application/json

{
  "name": "João Silva Santos",
  "email": "joao.novo@example.com",
  "phoneNumber": "(11) 91234-5678"
}
```

**Resposta**: `204 No Content` ou `404 Not Found`

### Deletar Cliente
```http
DELETE /customers/{customerId}
```

**Resposta**: `204 No Content` ou `404 Not Found`

## ⚙️ Configuração

### application.properties

```properties
spring.application.name=CustomerConnect
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=user
spring.datasource. password=123
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.show-sql=true
```

### Docker Compose

O arquivo `docker/docker-compose.yml` configura o MySQL: 

```yaml
services:
  mysql:
    container_name: 'customers-mysql'
    image: 'mysql:latest'
    environment:
      - 'MYSQL_DATABASE=mydatabase'
      - 'MYSQL_PASSWORD=123'
      - 'MYSQL_ROOT_PASSWORD=123'
      - 'MYSQL_USER=user'
    ports: 
      - '3306:3306'
```

## 🧪 Testes

```bash
./mvnw test
```

## 📝 Notas de Desenvolvimento

- A aplicação utiliza **Hibernate** com `ddl-auto=update` para criar/atualizar automaticamente o schema do banco
- Os timestamps (`createdAt` e `updatedAt`) são gerenciados automaticamente pelo Hibernate
- CPF e Email possuem constraint de **unicidade** no banco de dados
- A ordenação padrão é por data de criação (`createdAt`)


## 👨‍💻 Autor

Desenvolvido por [matalvesdev](https://github.com/matalvesdev)

## 📄 Licença

Este projeto está sob a licença MIT.  Veja o arquivo LICENSE para mais detalhes.

---

⭐ Se este projeto foi útil para você, considere dar uma estrela! 

