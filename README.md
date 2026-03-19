# 🚗 Sistema de Locadora de Veículos

## 📌 Sobre o Projeto

Este projeto tem como objetivo desenvolver um **banco de dados relacional** para gerenciar uma locadora de veículos.

O sistema permite controlar:

* Motoristas
* Clientes
* Veículos
* Aluguéis
* Multas
* Manutenções

---

## 🎯 Objetivo

Criar uma estrutura de banco de dados eficiente e consistente, garantindo:

* Integridade dos dados
* Relacionamentos corretos
* Facilidade de consulta e manutenção

---

## 👥 Público-alvo

* Empresas de locação de veículos
* Desenvolvedores iniciantes em banco de dados
* Estudantes de tecnologia

---

## 🗂️ Modelo de Dados (MER)

```mermaid
erDiagram

    MOTORISTA {
        int id PK
        string nome
        string cpf UNIQUE
        date data_nascimento
        string cnh UNIQUE
        date validade_cnh
        string telefone
        string email UNIQUE
        string endereco
        string status
        timestamp criado_em
    }

    CLIENTE {
        int id PK
        string nome
        string cpf UNIQUE
        string email UNIQUE
        string telefone
    }

    ATENDENTE {
        int id PK
        string nome
        string cpf UNIQUE
        string email UNIQUE
        string senha
        string nivel_acesso
    }

    CATEGORIA_VEICULO {
        int id PK
        string nome
        string descricao
    }

    STATUS_VEICULO {
        int id PK
        string nome
    }

    VEICULO {
        int id PK
        string modelo
        string placa UNIQUE
        int ano
        string chassi UNIQUE
        string cor
        int categoria_id FK
        int status_id FK
        decimal valor_diaria
        int quilometragem
        timestamp criado_em
    }

    ALUGUEL {
        int id PK
        int motorista_id FK
        int veiculo_id FK
        int atendente_id FK
        int cliente_id FK
        date data_inicio
        date data_fim
        date data_pagamento
        string forma_pagamento
        decimal valor_total
        string status
        string comprovante_url
        timestamp criado_em
    }

    MANUTENCAO {
        int id PK
        int veiculo_id FK
        string descricao
        date data_inicio
        date data_fim
        decimal custo
        string tipo
    }

    MULTA {
        int id PK
        int aluguel_id FK
        string descricao
        decimal valor
        date data_multa
        string status
    }

    MOTORISTA ||--o{ ALUGUEL : realiza
    CLIENTE ||--o{ ALUGUEL : solicita
    ATENDENTE ||--o{ ALUGUEL : registra
    VEICULO ||--o{ ALUGUEL : utilizado_em

    VEICULO ||--o{ MANUTENCAO : possui
    ALUGUEL ||--o{ MULTA : gera

    CATEGORIA_VEICULO ||--o{ VEICULO : classifica
    STATUS_VEICULO ||--o{ VEICULO : define
```

---

## 🧱 Estrutura do Projeto

```id="y7y2gs"
📁 scripts/
 ├── create_table_motorista.sql
 ├── create_table_cliente.sql
 ├── create_table_veiculo.sql
 ├── create_table_aluguel.sql
 ├── insert_into_motorista.sql
 ├── insert_into_veiculo.sql
 ├── insert_into_aluguel.sql
```

---

## ⚙️ Tecnologias Utilizadas

* PostgreSQL
* SQL (DDL e DML)
* GitHub

---

## 🛠️ Funcionalidades do Banco

* Cadastro de motoristas, clientes e atendentes
* Controle de veículos
* Registro de aluguéis
* Controle de multas
* Histórico de manutenções

---

## 🔁 Execução dos Scripts

Os scripts foram desenvolvidos para serem executados múltiplas vezes sem erro, utilizando:

* `CREATE TABLE IF NOT EXISTS`
* `CREATE OR REPLACE`

---

## 🚀 Como Executar

1. Criar o banco no PostgreSQL
2. Executar os scripts da pasta `scripts`
3. Inserir dados com os arquivos de INSERT
4. Testar com UPDATE e DELETE

---

## 📌 Observações

* Todas as tabelas possuem chaves primárias e estrangeiras
* Foram aplicadas restrições de integridade (NOT NULL, UNIQUE)
* O modelo segue boas práticas de banco relacional

---

## 👨‍💻 Autor

Projeto desenvolvido para fins acadêmicos.
