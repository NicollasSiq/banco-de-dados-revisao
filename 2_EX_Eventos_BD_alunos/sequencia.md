# Resolução

## Implementação SQL

### 1. Criação do Banco de Dados

```sql
-- Criação do banco de dados
CREATE DATABASE eventos_academicos CHARACTER SET utf8mb4;


-- Seleciona o banco de dados
ALTER TABLE eventos
ADD CONSTRAINT fk_palestrantes_eventos
FOREIGN KEY (Palestrante_id) REFERENCES palestrantes(id);

ALTER TABLE inscricoes
ADD CONSTRAINT fk_inscriçoes_eventos
FOREIGN KEY (Evento_ID) REFERENCES eventos(id);

```

### 2. Criação das Tabelas

```sql
-- Tabela de palestrantes
CREATE TABLE palestrantes (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    especialidade VARCHAR (50) NOT NULL,
    email VARCHAR (150) NOT NULL,
);





-- Tabela de eventos
CREATE TABLE eventos (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(100) NOT NULL,
    data_evento VARCHAR (100) NOT NULL,
    lugar VARCHAR (200) NOT NULL,
    capacidade DEFAULT,
    palestrante_id INT NOT NULL
);





-- Tabela de inscrições
CREATE TABLE inscricoes (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    evento_id INT NOT NULL,
    nome_participante VARCHAR (100) NOT NULL,
    email VARCHAR (200) NOT NULL,
    data_inscricao TIMESTAMP default CURRENT_TIMESTAMP,
    presente TINYINT,
);





```

### 3. Inserção de Dados Iniciais

```sql
-- Inserir palestrantes
INSERT INTO palestrantes (nome, especialidade, email)
VALUES ('Maria Silva', 'especialista em Inteligência Artificial' , 'maria@exemplo.com');

INSERT INTO palestrantes (nome, especialidade, email)
VALUES ('João Santos', 'especialista em Marketing Digital' , 'joao@exemplo.com');


-- Inserir eventos
INSERT INTO eventos (titulo, data_evento, lugar, capacidade, palestrante_id)
VALUES ('Workshop de IA', 'data: 15/11/2023', 'lugar: Auditório Principal', '100', 'palestrante: Maria Silva');

INSERT INTO eventos (titulo, data_evento, lugar, capacidade, palestrante_id)
VALUES ('Conferência de Marketing', 'data: 10/12/2023', 'lugar: Sala de Convenções', '200' , '2';)



-- Inserir algumas inscrições
INSERT INTO inscricoes (evento_id, nome_participante, email, data_inscricao, presente)
VALUES ('Workshop de IA', 'Carlos Oliveira','carlos@email.com');

INSERT INTO inscricoes (evento_id, nome_participante, email, data_inscricao, presente)
VALUES ('Workshop de IA', 'Carlos Oliveira','carlos@email.com');

INSERT INTO inscricoes (evento_id, nome_participante, email, data_inscricao, presente)
VALUES ('Workshop de IA', 'Ana Souza', 'ana@email.com');

INSERT INTO inscricoes (evento_id, nome_participante, email, data_inscricao, presente)
VALUES ('Conferência de Marketing', 'Bruno Lima', 'bruno@email.com');



```

### 4. View para Consulta

```sql
-- View para listar eventos com detalhes
CREATE VIEW vw_eventos_detalhados AS
SELECT 
    e.id,
    e.titulo,
    e.data_evento,
    e.local,
    e.capacidade,
    p.nome AS palestrante,
    p.especialidade,
    COUNT(i.id) AS total_inscritos,
    e.capacidade - COUNT(i.id) AS vagas_disponiveis
FROM 
    eventos e
LEFT JOIN 
    palestrantes p ON e.palestrante_id = p.id
LEFT JOIN 
    inscricoes i ON e.id = i.evento_id
GROUP BY 
    e.id, e.titulo, e.data_evento, e.local, e.capacidade, p.nome, p.especialidade;

-- Consultar a view
SELECT * FROM vw_eventos_detalhados;
```

### 5. Consultas Úteis

```sql
-- 1. Listar todos os eventos com suas respectivas informações
    SELECT  titulo, local_, capacidade, Data_evento, Palestrante_id
    FROM eventos


-- 2. Mostrar apenas eventos com vagas disponíveis (usando a view criada)
SELECT id, titulo, data_evento, local, vagas_disponiveis 
FROM vw_eventos_detalhados
WHERE vagas_disponiveis > 0;

-- 3. Listar participantes inscritos em um evento específico
    SELECT  Evento_ID, Nome_participante, Email
FROM inscriçoes
WHere Evento_ID = 1


```
