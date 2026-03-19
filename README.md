# 🚗 Sistema de Locação de Veículos

## 📋 Apresentação do Projeto

### Tema
Sistema de gerenciamento para locadora de veículos, permitindo o controle completo de motoristas, veículos, aluguéis, manutenções e multas.

### Objetivo Geral
Desenvolver um banco de dados relacional para gerenciar as operações de uma locadora de veículos, incluindo cadastro de motoristas, controle de frota, registro de aluguéis, manutenções e multas, garantindo a integridade e consistência dos dados.

### Público-Alvo
- Administradores de locadoras de veículos
- Atendentes e operadores do sistema
- Gerentes de frota
- Clientes que alugam veículos

---

## 📊 Modelo de Dados Relacional

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
        timestap criado_em
    }

    VEICULO {
        int id
        string modelo
        string placa
        int ano
        string chassi
        string cor
        int categoria_id
        int status_id
        decimal valor_diaria
        int quilometragem
        timestap criado_em
    }

    ALUGUEL {
        int id
        int motorista_id
        int veiculo_id
        int atendente_id
        int cliente_id
        date data_inicio
        date data_fim
        date data_pagamento
        string forma_pagamento
        decimal valor_total
        string status
        string comprovante_url
        timestap criado_em
    }

    MANUTENCAO {
        int id
        int veiculo_id
        string descricao
        date data_inicio
        date data_fim
        decimal custo
        string tipo
    }

    MULTA {
        int id
        int aluguel_id
        string descricao
        decimal valor
        date data_multa
        string status
    }

    CATEGORIA_VEICULO {
        int id
        string nome
        string descricao
    }

    STATUS_VEICULO {
        int id
        string nome
    }

    ATENDENTE {
        int id
        string nome
        string cpf
        string email
        string senha
        string nivel_acesso
    }

    CLIENTE {
        int id
        string nome
        string cpf
        string email
    }

    MOTORISTA ||--o{ ALUGUEL : realiza
    VEICULO ||--o{ ALUGUEL : alugado_em
    ATENDENTES ||--o{ ALUGUEL : registra
    CLIENTES ||--o{ ALUGUEL : vinculado
    
    VEICULO ||--o{ MANUTENCAO : possui
    ALUGUEL ||--o{ MULTA : pode_ter

    CATEGORIA_VEICULO ||--o{ VEICULO : classifica
    STATUS_VEICULO ||--o{ VEICULO : define
