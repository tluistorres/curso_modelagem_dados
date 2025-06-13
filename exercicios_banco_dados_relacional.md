## Exercícios Banco de Dados Relacional -Álgebra Relacional, Cálculo Relacional e Linguagem SQL

***Exercício 2.1 - Considere a chave estrangeira professor.codigo_depto.***
  
   Explique quais verificações devem ser realizadas pelo SGBD, quando:

    a. uma linha da tabela departamento for incluída,

    b. uma linha da tabela professor for excluída,

    c. a chave estrangeira professor.codigo_depto for alterada para um valor vazio.

departamento                                  
| codigo_depto        | nome_depto       | nivel_depto       | 
|---------------------|------------------|-------------------|
|        1            | Informática      | Pós-graduação     | 
|        2            | Administração    | Graduação         | 
|        3            | Medicina         | Graduação         |

Resp.: Nenhuma das operações listadas é capaz de levar o banco de dados a um estado inconsistente em relação à chave estrangeira considerada. Portanto, sua execução mão exige nenhuma verificação por parte do SGBD com referência à chave estrangeira do exemplo.


empregado                               
|   codigo_empregado  |       nome       |  cod_emp_chefe  |  
|---------------------|------------------|-----------------|
|         10          |     Pereira      |       NULL      | 
|         21          |     Tavares      |        10       | 
|         30          |     Satos        |        10       |
|         55          |     Almeida      |        21       | 

**Figura 2.7: Chave estrangeira que referencia a própria tabela.**


**Exercício 2.2 - Considere a chave estrangeira **empregado.cod_emp_chefe**(Figura 2.7). Liste quais são as operações de alteração do conteúdo desta tabela (inclusões, exclusões e alterações) nas quais o SGBD deve executar uma verificação para manter esta restrição de integridade. Em cada caso descreva a verificação que deve ser efetuada pelo SGBD.

Resp.: Para manter a integridade específica pela chave estrangeira **empregado.cod_emp_chefe**, o SGBD deve executar as seguintes verificações:

     - Quando da inclusão de uma linha na tabela;

       Neste caso, deve ser garantido que, caso seja informado um valor para cod_emp_chefe na linha incluída, este valor apareça na coluna codigo_emp.

     - Quando da alteração de cod_emp_chefe para um valor não vazio;

       Deve ser garantido que o novo valor do campo cod_emp_chefe apareça na coluna cod_emp.

     - Quando da exclusão de uma linha na tabela;

       Deve ser garantido que, na coluna cod_emp_chefe não apareça o valor do campo cod_emp da linha que está sendo excluída.

     - Quando da alteração do cod_emp;

       Deve ser garantido que, na coluna cod_emp-chefe, não apareça o antigo valor do campo codigo_emp.

 departamento                             
|   codigo_depto      |       nome       |  
|---------------------|------------------|
|        100          |     Vendas       |      
|        101          |   Financeiro     |        
|        102          |    Produção      |        
   


empregado                               
|   codigo_empregado  |       nome       |    cod_depto    | cod_emp_chefe  |  
|---------------------|------------------|-----------------|----------------|
|         10          |     Pereira      |      100        |      NULL      |
|         21          |     Tavares      |      101        |       10       |
|         30          |     Satos        |      100        |       10       |
|         55          |     Almeida      |      102        |       21       |

**Tabela 2.9: Tabelas para o exercício 2.3.** -> p.45.


**Exercício 2.3: Considere o banco de dados da **Figura 2.9**. Considere que existam duas chaves estrangeiras:

      - empregado.codigo_depto referencia departamento, e
      - empregado.cod_em_chefe referncia empregado.

Considere que a coluna empregado.cod_emp_chefe é opcional e que as demais colunas são obrigatórias.
      Represente o esquema deste banco de daddos na notação introduzida nesta seção.

Resp.: 
                                                                                                                    
                          

Tabela Departamento
| departamento |
|--------------|
| codigo_dpto  |
| nome         |

↔️ Relacionamento (1:N)

Tabela Empregado
| empregado      |
|----------------|
| cod_emp        |
| nome           |
| codigo_depto   |

   
     Observa-se a notação usada parta indicar a auto-referência na tabela empregado.
     Para diferenciar as duas chaves estrangeiras existentes na tabela empregado, usam-se os rótulos 'fk1' e 'fk2'. O fato de a coluna empregado.cod_emp_chefe ser opcional é indicada pelo rótulo 'n'.

 peca                              
|   codigo_peca      |    nome_peca     |    peso_peca    |    cor_peca    |     cidade_peca     |
|--------------------|------------------|-----------------|----------------|---------------------|
|         P1         |     Parafuso     |        5        |     Cinza      |    Porto Alegre     |
|         P2         |     Arruela      |        5        |     Cinza      |    Porto Alegre     |
|         P3         |     Mancal       |       25        |    Vermelho    |        Rio          |
|         P4         |      Eixo        |       15        |     Verde      |        Rio          |
|         P5         |     Motor        |       65        |    Vermelho    |        NULL        |

 embarque                              
|  codigo_fornec  |    cod_peca    |   data_embarq   |  qtde_embarq   |  
|-----------------|----------------|-----------------|----------------|
|         F1      |      P1        |   2000-01-12    |      300       |
|         F1      |      P1        |   2000-01-15    |      200       |
|         F1      |      P2        |   2000-01-12    |      350       |
|         F1      |      P3        |   2000-01-22    |      250       |
|         F1      |      P4        |   2000-01-12    |      150       |
|         F1      |      P5        |   2000-05-14    |      200       |
|         F2      |      P1        |   2000-01-12    |      300       |
|         F2      |      P1        |   2000-12-04    |      300       |
|         F2      |      P2        |   2000-12-04    |      350       |
|         F2      |      P3        |   2000-12-04    |      250       |
|         F2      |      P4        |   2000-09-24    |      150       |
|         F3      |      P2        |   2000-04-04    |      200       |
|         F3      |      P3        |   2000-10-30    |      350       |


 fornecedor            
|   cod_fornec        |  nome_fornec     |   status_fornec | cidade_fornec  |
|---------------------|------------------|-----------------|----------------|
|         F1          |   Antunes       |      5      |     Porto Alegre       |
|         F2      |     Silva     |      10     |      Porto Alegre    |
|         F3       |     Souza     |      15       |       Curitiba     |
|         F6      |     Antunes     |      10        |         Rio     |
|         F4      |     Machado      |       10        |     NULL       |
|         F5         |  Barcelos      |      12        |       Rio      |


**Figura 2.11: Possível conteúdo para o banco de dados de embarques.**

Exercício 2.4: Considere o banco de dados de embarques com o conteúdo mostrado na **Figura 2.11**. A chave primária da tabela embarque é composta pelas colunas cod_peca, cod_fornec e data_embarq.
      Justifique porque a chave primária da tabela não é composta somente pelas colunas cod_peca e cod_fornec.

Resp.: Caso a chave primária da tabela embarque fosse constituída apenas pelas colunas cod_pec e cod_fornec, a tabela não poderia conter múltiplas linhas de embarques de um mesmo fornecedor para uma mesma peça. Pelo conteúdo da tabela, isto pode acontecer, desde que os embarques ocorram em datas diferentes. Um exemplo são as duas primeiras linhas da tabela embarque.

 embarque                              
|  codigo_fornec  |    cod_peca    |   data_embarq   |  qtde_embarq   |  
|-----------------|----------------|-----------------|----------------|
|         F1      |      P1        |   2000-01-12    |      300       |
|         F1      |      P1        |   2000-01-15    |      200       |
|       ....      |                |                 |                |

Ambas as linhas referem-se ao mesmo fornecedor ('F1') e a mesma peça ('P1'),  mas têm diferentes datas de embarque.

Exercício 2.5: Considere o banco de dados de embarques com o conteúdo mostrado na **Figura 2.11**

      Com relação à chave primária da tabela embarque responda: É possível que existam dois embarques da mesma peça pelo mesmo fornecedor em uma determinada data? Justifique a resposta.

Exercício 2.6: Construa um esquema diagramático para o banco de dados acadêmico, usando a notação apresentada neste capítulo.


Exercício 2.7: Defina chaves alternativas para todas tabelas que compõe a variante do modelo acadêmico com chaves artificiais **(Figura 2.19)**.


Exercício 2.8: Deseja-se construir um banco de dados para armazenar informaões genealógicas. Neste banco de dados, pessoas armazenam informações sobre seus ancestrais e sobre descendentes destes.
      Cada pessoa é identificada por um código. Para cada pessoa, podem  ser armazenadas várias informações: sexo,
prenome, sobrenome, data e local de nascimento, bem como data e local de falecimento. Todas estas informações são opcionais. Cada local tem um código e um nome.
      Para cada união entre pessoas (casamento, união estável, ...), é necessário armazenar as seguintes informações:
pessoa que é marido, pessoa que é esposa, pessoas que são filhos gerados pela união e data e local da união.
Novamente, todas estas informações são opcionais.
      Uma pessoa pode ter participado de várias uniões.
      Deve ser projetado um banco de dados relacional para armazenar estes dados. O banco de dados deve refletir
exatamente o enunciado. Se necessário, podem ser criadas chaves prmárias artificiais. O banco de dados projetado não deve conter informações redundantes. Confeccione um esquema o banco de dados usando a notação diagramática vista neste capítulo.

Aqui está um esquema de banco de dados relacional para armazenar informações genealógicas:

Tabelas

1. Pessoa
    - id_pessoa (PK)
    - sexo
    - prenome
    - sobrenome
    - data_nascimento
    - id_local_nascimento (FK)
    - data_falecimento
    - id_local_falecimento (FK)

2. Local
    - id_local (PK)
    - nome

3. União
    - id_uniao (PK)
    - id_marido (FK)
    - id_esposa (FK)
    - data_uniao
    - id_local_uniao (FK)

4. Filho
    - id_uniao (FK)
    - id_pessoa (FK)

Relacionamentos

- Uma pessoa pode ter um local de nascimento e um local de falecimento (1:1 opcional)
- Uma pessoa pode participar de várias uniões (1:N)
- Uma união é entre duas pessoas (marido e esposa) (N:1)
- Uma união pode ter vários filhos (1:N)

Chaves

- id_pessoa é a chave primária da tabela Pessoa
- id_local é a chave primária da tabela Local
- id_uniao é a chave primária da tabela União
- A tabela Filho tem uma chave composta (id_uniao, id_pessoa)

Esse esquema de banco de dados reflete as informações necessárias para armazenar dados genealógicos, incluindo pessoas, locais, uniões e filhos. As chaves estrangeiras garantem a integridade dos dados e evitam informações redundantes.

Tabela Pessoa

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| id_pessoa | int | Código da pessoa |
| sexo | varchar | Sexo da pessoa |
| prenome | varchar | Prenome da pessoa |
| sobrenome | varchar | Sobrenome da pessoa |
| data_nascimento | date | Data de nascimento da pessoa |
| id_local_nascimento | int | Código do local de nascimento |
| data_falecimento | date | Data de falecimento da pessoa |
| id_local_falecimento | int | Código do local de falecimento |

Tabela Local

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| id_local | int | Código do local |
| nome | varchar | Nome do local |

Tabela União

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| id_uniao | int | Código da união |
| id_marido | int | Código do marido |
| id_esposa | int | Código da esposa |
| data_uniao | date | Data da união |
| id_local_uniao | int | Código do local da união |

Tabela Filho

| Campo | Tipo de Dado | Descrição |
| --- | --- | --- |
| id_uniao | int | Código da união |
| id_pessoa | int | Código da pessoa (filho) |

Chaves Primárias

- Pessoa: id_pessoa
- Local: id_local
- União: id_uniao
- Filho: (id_uniao, id_pessoa)

Chaves Estrangeiras

- Pessoa: id_local_nascimento → Local(id_local)
- Pessoa: id_local_falecimento → Local(id_local)
- União: id_marido → Pessoa(id_pessoa)
- União: id_esposa → Pessoa(id_pessoa)
- União: id_local_uniao → Local(id_local)
- Filho: id_uniao → União(id_uniao)
- Filho: id_pessoa → Pessoa(id_pessoa)

Essa representação mostra as tabelas com seus campos, tipos de dados e descrições, além das chaves primárias e estrangeiras que garantem a integridade dos dados.


# Relacionamentos


1. Pessoa - Local (Nascimento)
- Uma pessoa pode ter um local de nascimento (1:1 opcional)
- Tabela Pessoa tem uma chave estrangeira id_local_nascimento que referencia a tabela Local
1. Pessoa - Local (Falecimento)
- Uma pessoa pode ter um local de falecimento (1:1 opcional)
- Tabela Pessoa tem uma chave estrangeira id_local_falecimento que referencia a tabela Local
1. União - Pessoa (Marido)
- Uma união tem um marido (N:1)
- Tabela União tem uma chave estrangeira id_marido que referencia a tabela Pessoa
1. União - Pessoa (Esposa)
- Uma união tem uma esposa (N:1)
- Tabela União tem uma chave estrangeira id_esposa que referencia a tabela Pessoa
1. União - Local
- Uma união pode ter um local (1:1 opcional)
- Tabela União tem uma chave estrangeira id_local_uniao que referencia a tabela Local
1. União - Filho
- Uma união pode ter vários filhos (1:N)
- Tabela Filho tem chaves estrangeiras id_uniao e id_pessoa que referenciam as tabelas União e Pessoa, respectivamente

# SQL para criar as tabelas e relacionamentos

``` sqp

CREATE TABLE Local (
    id_local INT PRIMARY KEY,
    nome VARCHAR(255)
);

CREATE TABLE Pessoa (
    id_pessoa INT PRIMARY KEY,
    sexo VARCHAR(1),
    prenome VARCHAR(255),
    sobrenome VARCHAR(255),
    data_nascimento DATE,
    id_local_nascimento INT,
    data_falecimento DATE,
    id_local_falecimento INT,
    FOREIGN KEY (id_local_nascimento) REFERENCES Local(id_local),
    FOREIGN KEY (id_local_falecimento) REFERENCES Local(id_local)
);

CREATE TABLE Uniao (
    id_uniao INT PRIMARY KEY,
    id_marido INT,
    id_esposa INT,
    data_uniao DATE,
    id_local_uniao INT,
    FOREIGN KEY (id_marido) REFERENCES Pessoa(id_pessoa),
    FOREIGN KEY (id_esposa) REFERENCES Pessoa(id_pessoa),
    FOREIGN KEY (id_local_uniao) REFERENCES Local(id_local)
);

CREATE TABLE Filho (
    id_uniao INT,
    id_pessoa INT,
    PRIMARY KEY (id_uniao, id_pessoa),
    FOREIGN KEY (id_uniao) REFERENCES Uniao(id_uniao),
    FOREIGN KEY (id_pessoa) REFERENCES Pessoa(id_pessoa)
);

```

Obs.: Com os três acentos graves (``) e a especificação da linguagem (`sql), o código será renderizado corretamente no GitHub com a formatação e identação certas.

## Ágebra Relacional

empregado                               
|   codigo_empregado  |       nome       |    cod_depto    |  funcao   |      CPF      |     
|---------------------|------------------|-----------------|-----------|---------------|
|         E1          |     Souza        |      D1         |    <N>    |  13212133120  |
|         E2          |     Santos       |      D2         |     C5    |  89122111111  |
|         E3          |     Silva        |      D2         |     C5    |  34151177545  |
|         E5          |     Soares       |      D1         |     C2    |  63169275488  |

## Figura Tabela empregado com campo funcao vazio para o empregado

**Exemplo 3.17**(pag. 104) do Livro Banco de Dados Relacioanal.

Obter os dados do empregados cuja função é 'C5'. **Código em álbebra Relaciona?**

Para obter os dados dos empregados cuja função é 'C5', você pode usar a operação de seleção (σ) da álgebra relacional.

A expressão seria:

σ funcao = 'C5' (empregado)

Isso significa: "Selecione os tuplas da relação 'empregado' onde a função é igual a 'C5'".

O resultado será:

| codigo_empregado | nome | cod_depto | funcao |
|------------------|---------|-----------|--------|
| E2 | Santos | D2 | C5 |
| E3 | Silva | D2 | C5 |

Essa expressão retorna apenas as linhas da tabela onde a função é 'C5'.

Obs.: Obter os dados do empregados cuja função é 'C5'. **Código em SQL?**

Para obter os dados dos empregados cuja função é 'C5', você pode usar a seguinte consulta SQL:


SELECT *
FROM empregado
WHERE funcao = 'C5';


Essa consulta:

- SELECT * seleciona todas as colunas da tabela.
- FROM empregado especifica a tabela que você está consultando.
- WHERE funcao = 'C5' filtra os resultados para apenas as linhas onde a função é 'C5'.

O resultado seria:

| codigo_empregado | nome    | cod_depto | funcao |
|------------------|---------|-----------|--------|
| E2               | Santos  | D2        | C5     |
| E3               | Silva   | D2        | C5     |

Essa consulta retorna apenas as linhas da tabela onde a função é 'C5'.

**Exemplo 3.18**. Obter os dados dos empregados cuja função, quando informada (não vazia), é diferente de 'C2'**(Código em Álgebra Relacional).**

σ funcao ≠ 'C2' AND funcao ≠ NULL (empregado)

ou de forma mais comum:

σ funcao ≠ 'C2' AND funcao IS NOT NULL (empregado) ou σ funcao <>'C2' AND funcao IS NOT NULL (empregado)

Essa expressão significa:

- Selecione os tuplas da relação 'empregado' onde:
- A função é diferente de 'C2' (funcao ≠ 'C2')
- A função não é nula (funcao IS NOT NULL ou funcao ≠ NULL, dependendo da notação usada)
  
**σ funcao <> 'C2' AND funcao IS NOT NULL (empregado)**

A saída seria:

| codigo_empregado | nome    | cod_depto | funcao | CPF         |
|------------------|---------|-----------|--------|-------------|
| E2               | Santos  | D2        | C5     | 89122111111 |
| E3               | Silva   | D2        | C5     | 34151177545 |

**Exemplo 3.19**. Obter os dados dos empregados que tem função informada.

Álgebra Relacional:

σ funcao IS NOT NULL (empregado)

Essa expressão seleciona os tuplas da relação 'empregado' onde a função não é nula.

SQL:


SELECT *
FROM empregado
WHERE funcao IS NOT NULL;

Essa consulta seleciona todas as colunas da tabela 'empregado' onde a função não é nula.

Ambas as expressões retornam os empregados que têm uma função informada, ou seja, onde o campo "funcao" não é vazio ou nulo.

Com base na tabela que você forneceu anteriormente, a saída seria:

| codigo_empregado | nome    | cod_depto | funcao | CPF         |
|------------------|---------|-----------|--------|-------------|
| E2               | Santos  | D2        | C5     | 89122111111 |
| E3               | Silva   | D2        | C5     | 34151177545 |
| E5               | Soares  | D1        | C2     | 63169275488 |

Obs.: a saída da expressão:

 σ funcao = 'C5' (empregado) U σ funcao <> 'C5' (empregado) é:


| codigo_empregado | nome    | cod_depto | funcao | CPF         |
|------------------|---------|-----------|--------|-------------|
| E2               | Santos  | D2        | C5     | 89122111111 |
| E3               | Silva   | D2        | C5     | 34151177545 |
| E5               | Soares  | D1        | C2     | 63169275488 |

  - É a mesma saída que o código σ funcao IS NOT NULL (empregado), porque a união das duas condições (funcao = 'C5' e funcao <> 'C5') efetivamente seleciona todas as linhas que têm uma função não nula.
  
**Exemplo 3.19**. Obter os dados dos empregados cuja função é diferente de 'C2', inclusive daqueles que não tem função informada (campo funcao é NULL).

Para obter os dados dos empregados cuja função é diferente de 'C2', incluindo aqueles que não têm função informada (campo funcao é NULL), você pode usar a seguinte expressão em Álgebra Relacional:

 **σ funcao <> 'C2' OR funcao IS NULL (empregado)**

E em SQL:

SELECT *
FROM empregado
WHERE funcao <> 'C2' OR funcao IS NULL;

  - Saída:
  
| codigo_empregado | nome    | cod_depto | funcao | CPF         |
|------------------|---------|-----------|--------|-------------|
| E1               | Souza   | D1        | NULL   | 13212133120 |
| E2               | Santos  | D2        | C5     | 89122111111 |
| E3               | Silva   | D2        | C5     | 34151177545 |

**Exercício 3.21 (Banco de dados acadêmico) - Apêndice B --> p.555.**

 depto
| cod_depto | nome_depto | 
|-----------|------------|
| INF01   | Informática  | 
| MED01   | Medicina Interna | 
| MAT01   | Matemática   |
| FIS01   |   Física   |


 disciplina
| cod_depto  | num_disc  | nome_disc               | creditos_disc |
|------------|-----------|-------------------------|---------------|
| MAT01      | 101       | Cálculo Diferencial     | 4             |
| MAT01      | 102       | Álgebra Linear          | 4             |
| MAT01      | 103       | Geometria Analítica     | 4             |
| INF01      | 101       | Programação FORTRAN     | 4             |
| INF01      | 102       | Algoritmos e Programação| 6             |
| INF01      | 103       | Estrutura de Dados      | 4             |
| INF01      | 104       | Programação Lógica      | 4             |
| INF01      | 105       | Teoria da Computação    | 4             |
| INF01      | 106       | Banco de Dados          | 4             |
| INF01      | 107       | Linguagens Formais      | 2             |
| INF01      | 108       | Compiladores            | 4             |
| INF01      | 109       | Classificação e Pesquisa| 6             |


 prereq
| cod_epto   | num_disc  | num_disc | cod_depto_prereq  | num_disc_prereq |
|------------|-----------|----------|-------------------|-----------------|
| INF01      | 109       | 9        | INF01             | 107             | 
| INF01      | 109       | 9        | INF01             | 108             | 
| INF01      | 108       | 8        | INF01             | 106             | 
| INF01      | 108       | 8        | INF01             | 105             | 
| INF01      | 107       | 7        | INF01             | 104             | 
| INF01      | 106       | 6        | INF01             | 104             | 
| INF01      | 105       | 5        | INF01             | 104             | 
| INF01      | 104       | 4        | INF01             | 102             | 
| INF01      | 103       | 3        | INF01             | 102             | 
| MAT01      | 103       | 3        | MAT01             | 101             | 

**Figura 2.12: Conteúdo para o bancode dados acadêmico.**

  oferta
| ano_sem | cod_depto  | num_disc  | sigla_ofer | capacidade_ofer |
|---------|------------|-----------|------------|-----------------|
| 20211   | MAT01      | 101       | A          | 40              |
| 20211   | MAT01      | 101       | B          | 40              |
| 20211   | MAT01      | 101       | C          | 40              |
| 20211   | INF01      | 101       | A          | 40              |
| 20211   | INF01      | 101       | B          | 40              |
| 20211   | INF01      | 102       | A          | 20              |
| 20211   | INF01      | 102       | B          | 20              |
| 20211   | INF01      | 102       | C          | 20              |
| 20211   | INF01      | 103       | U          | 60              |
| 20211   | INF01      | 104       | U          | 40              |
| 20211   | INF01      | 105       | U          | 40              |
| 20211   | INF01      | 106       | A          | 30              |
| 20211   | INF01      | 106       | B          | 30              |
| 20021   | INF01      | 107       | U          | 70              |
| 20021   | INF01      | 108       | U          | 40              |
| 20021   | INF01      | 109       | U          | 40              |
| 20022   | MAT01      | 102       | A          | 40              |
| 20022   | MAT01      | 102       | B          | 40              |
| 20022   | MAT01      | 102       | C          | 40              |
| 20022   | INF01      | 101       | U          | 20              |
| 20022   | INF01      | 102       | A          | 20              |
| 20022   | INF01      | 102       | B          | 20              |
| 20022   | INF01      | 102       | C          | 20              |
| 20022   | INF01      | 103       | U          | 60              |
| 20022   | INF01      | 104       | U          | 40              |
| 20022   | INF01      | 105       | U          | 40              |
| 20022   | INF01      | 106       | U          | 70              |
| 20022   | INF01      | 107       | A          | 30              |
| 20022   | INF01      | 107       | B          | 40              |
| 20022   | INF01      | 109       | U          | 40              |

**Figura 2.13: Banco de dados acadêmico (tabela oferta)**


 predio
| cod_pred | nome_pred | 
|-----------|------------|
| 43421   | Informática -laboratórios  | 
| 43422  | Informática - administração | 
| 43423   | Informática - aulas   |


 sala
| cod_pred    | num_sala | descricao_sala | capacidade_sala |
|-------------|----------|---------------------|----------|
| 43421       | 101      | Laboratório Windows | 30       |
| 43421       | 102      | Laboratório Redes   | 30       |
| 43421       | 103      | Laboratório Linux   | 30       |
| 43421       | 104      | Laboratório Windows | 30       |
| 43421       | 105      | Laboratório Linux   | 30       |
| 43421       | 106      | Laboratório Hardware | 30       |
| 43421       | 107      | Laboratório Automação | 30      |
| 43422       | 101      | Secretaria Geral    | NULL      |
| 43422       | 102      | Secretaria Graduação | NULL     |
| 43422       | 103      | Secretaria pós´graduação | NULL |
| 43423       | 101      | Sala de aula comun | 30    |
| 43423       | 102      | Sala de aula comu | 30   |
| 43423       | 103      | Sala de aula comun | 30  | 
| 43423       | 104      | Sala de aula multimídia | 30  |
| 43423       | 105      | Auditório | 80   |
| 43423       | 106      | Sala de aula laboratório | 30  |
| 43423       | 107      | Sala de aula laboratório | 30 |


**Figura 2.14: Banco de dados acadêmico.**

 
 periodo
| ano_sem | cod_ dpto | num_disc | sigla_ofer | dia_sem | hora_início | cod_pred | num_sala | num_horas |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| 20021 | MAT01 | 101 | A | 2 | 8 | 43423 | 101 | 2 |  
| 20021 | MAT01 | 101 | A | 4 | 8 | 43423 | 101 | 2 |  
| 20021 | MAT01 | 101 | B | 2 | 10 | 43423 | 101 | 2 |  
| 20021 | MAT01 | 101 | B | 4 | 10 | 43423 | 101 | 2 |  
| 20021 | MAT01 | 101 | C | 2 | 8 | 43423 | 102 | 2 |  
| 20021 | MAT01 | 101 | C | 4 | 8 | 43423 | 102 | 2 |  
| 20021 | INF01 | 101 | A | 2 | 8 | 43421 | 102 | 2 |  
| 20021 | INF01 | 101 | A | 4 | 8 | 43421 | 102 | 2 |  
| 20021 | INF01 | 101 | B | 2 | 10 | 43421 | 102 | 2 |  
| 20021 | INF01 | 101 | B | 4 | 10 | 43421 | 102 | 2 |  
| 20021 | INF01 | 102 | A | 2 | 8 | 43421 | 101 | 2 |  
| 20021 | INF01 | 102 | A | 4 | 8 | 43421 | 103 | 2 |  
| 20021 | INF01 | 102 | A | 6 | 8 | 43421 | 103 | 2 |  

**Figura 2.15: Banco de dados acadêmico.**


 departamento
| codigo_depto    | nome_dpto     | nivel_dpto    | 
|-----------------|---------------|---------------|
| 1               | Informática   | Pós-graduação | 
| 2               | Administração | Graduação     | 
| 3               | Medicina      | Graduação     |

 professor
| codigo_prof | nome_prof     | titulacao_prof | cod_dpto |
|-------------|---------------|----------------|----------|
| 1           | Antônio Souza | Doutor          | 1       |
| 2           | Pedro Silva   | Mestre          | 2       |
| 3           | Felipe Souza  | Doutor          | 3       |
| 4           | Manuel Silva  | Doutor          | 1       |

**Figura 1.1: Arquivos em um banco de dados de uma universidade**

    Modelo Conceitual
Departamento
| Atributo | Descrição |
| --- | --- |
| Cod_depto (PK) | Código do departamento |
| Nome_dpto | Nome do departamento |
| nivel_dpto | Nível do departamento |

Professor
| Atributo | Descrição |
| --- | --- |
| Cod_Prof (PK) | Código do professor |
| Nome_Prof | Nome do professor |
| titulacao_prof | Titulação do professor |
| codigo_depto (FK) | Código do departamento |

Relacionamento
- Pertence a: Um professor pertence a um departamento (N:1)


**Figura 1.2: Exemplo de modelo conceitual**


| departamento |
|-------------|
| Cod_depto | 
| Nome_dpto | 
| nivel_dpto   | 

| Professor |
|-----------|
| Cod_Prof | 
| Nome_Prof | 
| titulacao_prof  | 
| codigo_depto    | 

**Figura 1.3: Esquema gráfico para o banco de dados.**


 titulacao
| cod_tit | nome_tit | 
|-----------|------------|
| 1   | Graduado  | 
| 2   | Especialista | 
| 3   | Mestre   |
| 4   |  Doutor   |


 professor
| cod_prof    | cod_depto | cod_tit | nome_prof |
|-------------|----------|---------------------|----------|
| 1       | INF01      | 4 | Souza       |
| 2       | INF01     | 4   | Antunes       |
| 3       | INF01      | 4   | Macedo       |
| 4       | INF01      | NULL | Machado       |
| 5       | INF01      | 3   | Tavares       |
| 6       | INF01      | 3 | Pereira       |
| 7       | MAT01      | 4 | Alvares      |
| 8       | MAT01      | 4    | Silva      |
| 9       | MAT01      | NULL | Souza     |
| 10      | INF01      | NULL | Machado |
| 11      | INF01      | 4 | Moreira    |

**Figura 2.16: Banco de dados acadêmico.**


 prof_oferta
| ano_sem | cod_ dpto | num_disc | sigla_ofer | cod_prof |
| --- | --- | --- | --- | --- |  
| 20021 | MAT01 | 101 | A | 10 |
| 20021 | MAT01 | 101 | A | 11 |   
| 20021 | MAT01 | 101 | A | 2 |  
| 20021 | MAT01 | 101 | B | 7 |   
| 20021 | MAT01 | 101 | C | 8 |  
| 20021 | INF01 | 101 | A | 4 |  
| 20021 | INF01 | 101 | A | 5 |   
| 20021 | INF01 | 101 | B | 1 |   
| 20021 | INF01 | 102 | A | 2 |   
| 20021 | INF01 | 102 | B | 3 |   
| 20021 | INF01 | 102 | C | 6 |  
| 20021 | INF01 | 102 | C | 5 |   
| 20021 | INF01 | 103 | U | 7 |  
| 20021 | MAT01 | 104 | U | 4 |
| 20021 | MAT01 | 105 | U | 2 |   
| 20021 | MAT01 | 106 | A | 3 |  
| 20021 | MAT01 | 106 | B | 6 |   
| 20021 | MAT01 | 107 | U | 5 |  
| 20021 | INF01 | 108 | U | 4 |  
| 20021 | INF01 | 109 | U | 5 |   
| 20021 | INF01 | 102 | A | 3 |   
| 20021 | INF01 | 102 | B | 6 |   
| 20021 | INF01 | 102 | C | 5 |   
| 20021 | INF01 | 101 | U | 2 |  
| 20021 | INF01 | 102 | A | 6 |   
| 20021 | INF01 | 102 | B | 1 |  
| 20021 | INF01 | 102 | C | 2 | 
| 20021 | INF01 | 103 | U | 3 |   
| 20021 | INF01 | 104 | U | 2 |    
| 20021 | INF01 | 105 | U | 1 |   
| 20021 | INF01 | 106 | U | 6 |   
| 20021 | INF01 | 107 | A | 3 |  
| 20021 | INF01 | 107 | B | 4 |   
| 20021 | INF01 | 109 | U | 3 |  


**Figura 2.17: Banco de dados acadêmico.** - p.57

**Exercício 3.25: Usando álgebra relacional, escreva uma consulta que obtenha os códigos e os nomes dos departamentos que, em 20021, tiveram ao menos uma oferta com aulas nas segundas-feiras (dia_sem=2), na sala 101 do prédio denominado 'Informática - laboratórios'.**
     
(De acordo com o livro Banco de Dados Relacional)

π depto.cod_depto, depto.nome_depto 
( σ  depto.cod_depto = periodo.cod_depto
 AND periodo.cod_pred = predio.cod_pred
 AND periodo.ano_sem = 20021
 AND periodo.dia_sem =2
 AND periodo.num_sala = 101
 AND periodo.nome_pred = 
          ' Informática - laboratórios '
    ( depto x
      periodo x
      predio   
    )  
)

(De acordo com o Chat da Meta)

π depto.cod_depto, depto.nome_depto (
σ depto.cod_depto = periodo.cod_depto 
AND periodo.cod_pred = predio.cod_pred 
AND predio.nome_pred = 'Informática - laboratórios' 
AND periodo.ano_sem = 20021 AND periodo.dia_sem = 2 
AND periodo.num_sala = 101 (
depto x periodo x predio
)
)

**SQL:**

SELECT DISTINCT d.cod_depto, d.nome_depto
FROM depto d
JOIN periodo p ON d.cod_depto = p.cod_dpto
JOIN predio pr ON p.cod_pred = pr.cod_pred
WHERE pr.nome_pred = 'Informática - laboratórios'
  AND p.ano_sem = 20021
  AND p.dia_sem = 2
  AND p.num_sala = 101;


**Cálculo Relacional:**

{t | ∃d ∈ Depto ∃p ∈ Periodo ∃pr ∈ Predio (
d.cod_depto = p.cod_dpto ∧ p.cod_pred = pr.cod_pred ∧
pr.nome_pred = 'Informática - laboratórios' ∧
p.ano_sem = 20021 ∧ p.dia_sem = 2 ∧ p.num_sala = 101
) ∧ t.cod_depto = d.cod_depto ∧ t.nome_depto = d.nome_depto}

Ou, de forma mais compacta:
{t | ∃d ∈ Depto ∃p ∈ Periodo ∃pr ∈ Predio (
d.cod_depto = p.cod_dpto ∧ p.cod_pred = pr.cod_pred ∧
pr.nome_pred = 'Informática - laboratórios' ∧ p.ano_sem = 20021 ∧ p.dia_sem = 2 ∧ p.num_sala = 101
) ∧ t = <d.cod_depto, d.nome_depto>}

Ambos os códigos buscam os departamentos que atendem às condições especificadas e retornam os códigos e nomes dos departamentos.