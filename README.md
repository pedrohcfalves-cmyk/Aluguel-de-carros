-- =========================
-- TABELAS AUXILIARES
-- =========================

CREATE TABLE IF NOT EXISTS categoria_veiculo (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao TEXT
);

CREATE TABLE IF NOT EXISTS status_veiculo (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

-- =========================
-- PESSOAS
-- =========================

CREATE TABLE IF NOT EXISTS motorista (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    data_nascimento DATE NOT NULL,
    cnh VARCHAR(20) UNIQUE NOT NULL,
    validade_cnh DATE NOT NULL,
    telefone VARCHAR(20),
    email VARCHAR(150) UNIQUE,
    endereco TEXT,
    status VARCHAR(50),
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS cliente (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    email VARCHAR(150) UNIQUE,
    telefone VARCHAR(20)
);

CREATE TABLE IF NOT EXISTS atendente (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    senha TEXT NOT NULL,
    nivel_acesso VARCHAR(50) NOT NULL
);

-- =========================
-- VEICULO
-- =========================

CREATE TABLE IF NOT EXISTS veiculo (
    id SERIAL PRIMARY KEY,
    modelo VARCHAR(100) NOT NULL,
    placa VARCHAR(10) UNIQUE NOT NULL,
    ano INT NOT NULL,
    chassi VARCHAR(50) UNIQUE NOT NULL,
    cor VARCHAR(50),
    categoria_id INT NOT NULL,
    status_id INT NOT NULL,
    valor_diaria DECIMAL(10,2) NOT NULL,
    quilometragem INT DEFAULT 0,
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_categoria
        FOREIGN KEY (categoria_id)
        REFERENCES categoria_veiculo(id),

    CONSTRAINT fk_status
        FOREIGN KEY (status_id)
        REFERENCES status_veiculo(id)
);

-- =========================
-- ALUGUEL
-- =========================

CREATE TABLE IF NOT EXISTS aluguel (
    id SERIAL PRIMARY KEY,
    motorista_id INT NOT NULL,
    veiculo_id INT NOT NULL,
    atendente_id INT NOT NULL,
    cliente_id INT NOT NULL,
    data_inicio DATE NOT NULL,
    data_fim DATE NOT NULL,
    data_pagamento DATE,
    forma_pagamento VARCHAR(50),
    valor_total DECIMAL(10,2) NOT NULL,
    status VARCHAR(50),
    comprovante_url TEXT,
    criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_motorista
        FOREIGN KEY (motorista_id)
        REFERENCES motorista(id),

    CONSTRAINT fk_veiculo
        FOREIGN KEY (veiculo_id)
        REFERENCES veiculo(id),

    CONSTRAINT fk_atendente
        FOREIGN KEY (atendente_id)
        REFERENCES atendente(id),

    CONSTRAINT fk_cliente
        FOREIGN KEY (cliente_id)
        REFERENCES cliente(id)
);

-- =========================
-- MANUTENCAO
-- =========================

CREATE TABLE IF NOT EXISTS manutencao (
    id SERIAL PRIMARY KEY,
    veiculo_id INT NOT NULL,
    descricao TEXT NOT NULL,
    data_inicio DATE NOT NULL,
    data_fim DATE,
    custo DECIMAL(10,2),
    tipo VARCHAR(50),

    CONSTRAINT fk_manutencao_veiculo
        FOREIGN KEY (veiculo_id)
        REFERENCES veiculo(id)
);

-- =========================
-- MULTA
-- =========================

CREATE TABLE IF NOT EXISTS multa (
    id SERIAL PRIMARY KEY,
    aluguel_id INT NOT NULL,
    descricao TEXT,
    valor DECIMAL(10,2) NOT NULL,
    data_multa DATE NOT NULL,
    status VARCHAR(50),

    CONSTRAINT fk_multa_aluguel
        FOREIGN KEY (aluguel_id)
        REFERENCES aluguel(id)
);
