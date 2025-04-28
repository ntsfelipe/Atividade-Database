``` sql
CREATE TABLE alunos (
id SERIAL PRIMARY KEY,
nome TEXT NOT NULL,
nascimento DATE
);

CREATE TABLE curso (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  duracao_anos INT
);

CREATE TABLE matriculas (
  id SERIAL PRIMARY KEY,
  alunos_id INT references alunos(id) ON DELETE CASCADE,
  curso_id INT references curso(id) ON DELETE CASCADE,
  data_matricula DATE default CURRENT_DATE
);

ALTER TABLE alunos 
  add column curso TEXT NOT NULL;

ALTER TABLE alunos
drop column nascimento;

INSERT INTO alunos (nome, curso)
VALUES ('Felipe Neves', 'Engenharia de Software'),
('Rafael Cabral', 'Engenharia da Computação'),
('Carlos Eduardo', 'Engenharia de Software'),
('Luiz Felipe', 'Ciência da Computação'),
('Paulo Vitor', 'Sistemas de Informação');

INSERT INTO curso (nome, duracao_anos)
VALUES ('Engenharia de Software', 4),
('Engenharia da Computação', 4),
('Ciência da Computação', 4),
('Sistemas de Informação', 4),
('ADM Tech', 4);

INSERT INTO matriculas (alunos_id, curso_id)
VALUES (1, 1),
       (2, 2);

INSERT INTO matriculas (alunos_id, curso_id)
VALUES (3, 3),
(4, 4),
(5, 4);

SELECT a.nome AS alunos, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.alunos_id = a.id
JOIN curso c ON m.curso_id = c.id;

INSERT INTO alunos (nome, curso)
VALUES ('Hugo Montan', 'ADM Tech'),
('Luana de Jesus', 'Sistemas de Informação'),
('Eduardo Jesus', 'Engenharia da Computação'),
('Yan de Oliveira', 'Ciência da Computação'),
('Christian Vinícius', 'Engenharia da Computação');

INSERT INTO matriculas (alunos_id, curso_id)
VALUES (6, 5),
(7, 4),
(8, 2),
(9, 3),
(10, 2);

SELECT a.nome AS alunos, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.alunos_id = a.id
JOIN curso c ON m.curso_id = c.id;

DELETE FROM alunos WHERE nome = 'Paulo Vitor';

INSERT INTO alunos (nome, curso)
VALUES ('Paulo Vitor', 'Sistemas de Informação');

INSERT INTO matriculas (alunos_id, curso_id)
VALUES (11, 4);

SELECT a.nome AS alunos, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.alunos_id = a.id
JOIN curso c ON m.curso_id = c.id;

```
