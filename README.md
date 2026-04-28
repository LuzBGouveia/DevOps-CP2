# Checkpoint 2 - DevOps

## Lucas Barros Gouveia - RM566422

---

## Sobre o Projeto

Este projeto faz parte do **Checkpoint 2 de DevOps** da FIAP. O objetivo é demonstrar o uso de **containers Docker** rodando em uma máquina virtual na nuvem da **Microsoft Azure**.

A aplicação foi projetada para execução via Docker e consiste em uma **API REST** de gerenciamento de transações financeiras, desenvolvida com **Spring Boot 3** e conectada a um banco de dados **MySQL 8**, onde ambos os serviços rodam como containers.

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
├── docs/                          # Screenshots da aplicação rodando na VM
├── transacoes-api/
│   ├── Dockerfile.api             # Imagem da API (build)
│   ├── pom.xml
│   └── src/                       # Código-fonte Spring Boot
└── mysql-dimdim/
    ├── Dockerfile.mysql           # Imagem do MySQL com banco e dados iniciais (build)
    └── docker-entrypoint-initdb.d/
        └── init.sql               # Criação da tabela e dados seed
```

## Como executar o projeto com bash

### 1. Clonar o repositório

```
git clone https://github.com/LuzBGouveia/DevOps-CP2
cd DevOps-CP2
```

### 2. Criando a rede do Docker
```
docker network create dimdim-network
```

### 3. Rodando o container do MySQL (aguarde alguns segundos após a inicialização)

```
cd mysql-dimdim

docker build -f Dockerfile.mysql -t mysql-dimdim .

docker run --name mysql-dimdim -d \
 --network dimdim-network \
 -p 3306:3306 \
 -v mysql-dimdim-data:/var/lib/mysql \
 mysql-dimdim

cd ..
```

### 4. Rodando o container da API

```
cd transacoes-api

docker build -f Dockerfile.api -t api-dimdim .

docker run --name api-dimdim -d \
 --network dimdim-network \
 -p 8080:8080 \
 api-dimdim

cd ..
```

### 5. Verificar containers em execução

```
docker ps
```


### 6. Testando endpoint

```
curl http://<IP da VM>:8080/transacoes
```
