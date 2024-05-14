# Microserviço de disparo de emails com mensageria.

Projeto desenvolvido para melhorar o conhecimento de Microserviços e de mensageria utilizando RabbitMQ e CloudAMQP.(Tem que criar a conta na CloudAMQP, caso não tenha)

O projeto contém dois bancos de dados (PostgreSQL) subidos no Docker. Todas as configurações para a completa funcionalidade desse projeto vai estar abaixo. 

## Java (versão)
- Java 17.0.11

## Spring Boot (versão)
- Spring Boot 3.2.5

## IDE
- IntelliJ

## Requisição HTTP
- Api Dog

## Adicionando dependências do Spring Boot
Aqui estão todas as dependências utilizadas

- Spring Web
- Spring Data JPA
- PostgreSQL Driver
- Validation
- Spring for RabbitMQ
- Java Mail Sender

## Configuração do Docker (PostgreSQL)

- User

```yml
services:
  postgres:
    container_name: user_postgres
    image: postgres
    ports:
      - 5432:5432
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=admin
      - POSTGRES_DB=user-ms
```

- Email

```yml
services:
  postgres:
    container_name: email_postgres
    image: postgres
    ports:
      - 5433:5432
    environment:
      - POSTGRES_USER=admin
      - POSTGRES_PASSWORD=admin
      - POSTGRES_DB=email-ms
```

## Configuração do application.properties

- User

```bash
spring.application.name=user

server.port=8081
spring.datasource.username=admin
spring.datasource.password=admin
spring.datasource.url=jdbc:postgresql://localhost:5432/user-ms
spring.jpa.hibernate.ddl-auto=update

spring.rabbitmq.addresses=sua url do cloudamqp

broker.queue.email.name=default.email
```

- Email

```bash
spring.application.name=email

server.port=8082
spring.datasource.username=admin
spring.datasource.password=admin
spring.datasource.url=jdbc:postgresql://localhost:5433/email-ms
spring.jpa.hibernate.ddl-auto=update

spring.rabbitmq.addresses=sua url do cloudamqp

broker.queue.email.name=default.email

spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=seuemail@email.com
spring.mail.password=suasenha123
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```
