#  Alteração de tabelas e tipos de variáveis

No dia 6 de Março, foi proposto uma atividade de Banco de Dados para criar 4 tabelas sem chaves primárias e estrangeiras, além de obrigatoriamente conter atributos do tipo decimal e date, e, em seguida, inserir manualmente as chaves.

# Como eu realizei

## Passo 1: Montei um planejamento de BD baseado em festa de aniversário:

![Planejamento do Banco de Dados](https://lh6.googleusercontent.com/dh9cVRu6z8QgslTxlAFMvuCZbO76vr8ON7yVHjMK1LZPzkFWdEluvGrwQ05NBCrdo0oIT5Rjy3bVL20=w2504-h962)

## Passo 2: Criando Banco de Dados PostgreSQL baseado no planejamento:

~~~postgresql
CREATE TABLE Aniversariante(
    nome VARCHAR(50) NOT NULL,
    idade int NOT NULL,
    altura DECIMAL(3,2) NOT NULL,
    dia_aniversario DATE NOT NULL
);

CREATE TABLE Convidado(
    nome VARCHAR(50) NOT NULL,
    foi_convidade BOOLEAN NOT NULL,
    tem_presente BOOLEAN NOT NULL
);

CREATE TABLE Presente(
    tipo VARCHAR(50) NOT NULL,
    descricao TEXT NOT NULL
);

CREATE TABLE organizador(
    CNPJ VARCHAR(20) NOT NULL,
    setor VARCHAR(50) NOT NULL,
    horario DATE NOT NULL
);
~~~

## Passo 3: Com o código acima, implementar as chaves primárias e estrangeiras:

~~~postgresql
CREATE TABLE Aniversariante(
    nome VARCHAR(50) NOT NULL,
    idade int NOT NULL,
    altura DECIMAL(3,2) NOT NULL,
    dia_aniversario DATE NOT NULL
);

CREATE TABLE Convidado(
    nome VARCHAR(50) NOT NULL,
    foi_convidade BOOLEAN NOT NULL,
    tem_presente BOOLEAN NOT NULL
);

CREATE TABLE Presente(
    tipo VARCHAR(50) NOT NULL,
    descricao TEXT NOT NULL
);
    CREATE TABLE organizador(
    CNPJ VARCHAR(20) NOT NULL,
    setor VARCHAR(50) NOT NULL,
    horario DATE NOT NULL
);

alter TABLE aniversariante add COLUMN CPF VARCHAR(20);
alter TABLE aniversariante add PRIMARY KEY (CPF);
alter TABLE convidado add COLUMN CPF VARCHAR(20);
alter TABLE convidado add PRIMARY KEY (CPF);

alter TABLE convidado add COLUMN CPF_aniversariante VARCHAR(20);

alter TABLE convidado add FOREIGN KEY (CPF_aniversariante)
REFERENCES Aniversariante(cpf);

alter TABLE presente add COLUMN Nota_fiscal VARCHAR(100);
alter TABLE presente add PRIMARY KEY(Nota_fiscal);
alter TABLE presente add COLUMN CPF_convidado VARCHAR(20);

alter TABLE presente add FOREIGN KEY(CPF_convidado) REFERENCES
convidado(CPF);

alter TABLE organizador add PRIMARY KEY CNPJ VARCHAR(20);

ALTER TABLE organizador ADD COLUMN CPF_aniversariante
VARCHAR(20);

alter TABLE organizador add FOREIGN KEY (CPF_aniversariante)
REFERENCES Aniversariante(cpf);
~~~

## Passo 4: Representar novo código em modelagem de banco de dados:

![Modelagem de Banco de dados](https://lh3.googleusercontent.com/PunHKkndd2eFwXWjbgqstAInrNwTPdPIUSt96LOVvM1X0Oeh_96SbLcnDwkbyCSVwVnNKuxgATDQsOQ=w2504-h962)