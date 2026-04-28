# Checkpoint 2 - DevOps

## Lucas Barros Gouveia - RM566422

---

## Sobre o Projeto

Este projeto faz parte do **Checkpoint 2 de DevOps** da FIAP. O objetivo é demonstrar o uso de **containers Docker** rodando em uma máquina virtuai na nuvem da **Microsoft Azure**.

A aplicação consiste em uma **API REST** de gerenciamento de transações financeiras, desenvolvida com **Spring Boot 3** e conectada a um banco de dados **MySQL 8**, onde ambos os serviços rodam como containers Docker.

## Endpoints da API

| Método | Endpoint | Descrição |
|---|---|---|
| GET | `/transacoes` | Lista todas as transações |
| GET | `/transacoes/{id}` | Busca transação por ID |
| POST | `/transacoes` | Cria nova transação |
| PUT | `/transacoes/{id}` | Atualiza transação |
| DELETE | `/transacoes/{id}` | Remove transação |

## Estrutura do Repositório

```
├── docs/                          # Screenshots da aplicação rodando nas VMs
├── transacoes-api/
│   ├── Dockerfile.api             # Imagem da API (multi-stage build)
│   ├── pom.xml
│   └── src/                       # Código-fonte Spring Boot
└── mysql-dimdim/
    ├── Dockerfile.mysql           # Imagem do MySQL com banco e dados iniciais
    └── docker-entrypoint-initdb.d/
        └── init.sql               # Criação da tabela e dados seed
```
