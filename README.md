### Criando um banco de dados 100% com SQL
---

> *Visando aprimorar os nossos conhecimentos em SQL, vamos criar um banco de dados do 0, criar algumas tabelas que se relacionem, ou sejá teremos a criação de chave estrangeira, e inserir dados nestas tabelas.*

---

* #### Criando o Banco de Dados

~~~sql
CREATE DATABASE ERP_Homol
(
	NAME		=	ERP_Homol -- Nome do DB
,	FILENAME	=	'C:\Data_Bases\ERP_Homol.md' -- Local onde o arquivo do DB será salvo
,	SIZE		=	12MB -- Tamanho inicial do DB
,	MAXSIZE		=	36MB -- Tamanho Máximo do DB
,	FILEGROWTH	=	10% -- Para especificar o incremento do tamanho máximo do DB
)
~~~

---

* #### Criando as Tabelas
> 1. **Tabela Funcionários**
~~~sql
CREATE TABLE Funcionarios (
	CODFUN		SMALLINT PRIMARY KEY IDENTITY NOT NULL -- Realiza o incremento automático do ID único
,	Nome		VARCHAR(15) NOT NULL
,	Sobrenome	VARCHAR(15) NOT NULL
,	DataNasc	DATE		NOT	NULL
,	DataContr	DATE		NOT NULL
,	Email		VARCHAR(30)
,	CODCAR		INT			NOT NULL -- Será transfomada em uma FOREIGN KEY separadamente
)
~~~
> 2. **Tabela Cargos**
~~~sql
CREATE TABLE Cargos (
	CODCAR INT PRIMARY KEY IDENTITY NOT NULL -- Realiza o incremento automático do ID único
,	Cargo	VARCHAR(20) NOT NULL
)
~~~

---

* #### Criando FOREIGN KEY
> *Cria na tabela Funcionários uma chave estrangeira na coluna CODCAR, onde podemos relacionar com a tabela Cargo*
~~~sql
ALTER TABLE Funcionarios ADD CONSTRAINT FK_FUNCIONARIOS FOREIGN KEY (CODCAR)
REFERENCES Cargos (CODCAR)
~~~

---

* #### Inserindo dados nas tabelas
~~~sql
INSERT INTO Cargos (Cargo)
VALUES ('CEO')
INSERT INTO Funcionarios (Nome,Sobrenome,DataNasc,DataContr,Email,CODCAR)
VALUES ('Jose','Silva','1959-11-18','2010-05-20','','1')
~~~
---

* #### SELECT para consultar os dados inseridos e ver se está tudo OK com o banco de dados criado

> 1. *Consulta Básica apenas **SELECT  FROM***
~~~sql
SELECT * FROM Funcionarios
SELECT * FROM Cargos
~~~
<img src = img/img1.png>

> 2. *Consulta utilizando o relacionamento entre as tabelas*
~~~sql
SELECT *
FROM Funcionarios F
INNER JOIN Cargos C WITH (NOLOCK) ON F.CODCAR = C.CODCAR
~~~
<img src = img/img2.png>



