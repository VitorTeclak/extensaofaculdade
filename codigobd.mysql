CREATE DATABASE IF NOT EXISTS empresa;
USE empresa;

CREATE TABLE operador (
    id_operador INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    nome VARCHAR(30) NOT NULL,
    turno VARCHAR(10)
);

CREATE TABLE defeitos (
    id_defeitos INT PRIMARY KEY AUTO_INCREMENT,
    tipos_de_defeito VARCHAR(20)
);

CREATE TABLE lote_cobre (
    id_lote INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    data_da_compra DATE,
    kg_comprado FLOAT
);

CREATE TABLE trefila (
    id_trefila INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    id_lote INT NOT NULL,
    id_defeitos INT,
    FOREIGN KEY (id_defeitos) REFERENCES defeitos(id_defeitos),
    FOREIGN KEY (id_lote) REFERENCES lote_cobre(id_lote)
);

CREATE TABLE ordem_de_producao (
    id_op INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    tipo_de_produto VARCHAR(50) NOT NULL,
    diametro FLOAT NOT NULL,
    bitola FLOAT NOT NULL,
    numero_de_fios INT NOT NULL,
    metragem_a_produzir INT,
    data_producao DATE,
    id_operador INT NOT NULL,
    id_lote INT,
    id_defeitos INT, 
    FOREIGN KEY (id_operador) REFERENCES operador(id_operador),
    FOREIGN KEY (id_lote) REFERENCES lote_cobre(id_lote),
    FOREIGN KEY (id_defeitos) REFERENCES defeitos(id_defeitos)
);

CREATE VIEW relatorio_diario AS 
SELECT 
    o.id_op,
    o.tipo_de_produto,
    o.diametro,
    o.numero_de_fios,
    o.metragem_a_produzir AS metragem_produzida,
    o.data_producao,
    p.nome AS operador,
    p.turno AS turno_produzido,
    o.id_lote AS cobre_utilizado,
    d.id_defeitos AS defeitos_apresentados
FROM ordem_de_producao o
INNER JOIN operador p ON o.id_operador = p.id_operador
LEFT JOIN lote_cobre l ON o.id_lote = l.id_lote
LEFT JOIN defeitos d ON o.id_defeitos = d.id_defeitos;
