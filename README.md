# Power-BI-Analyst
Business Intelligence and data analysis projects.

### Desafio de projeto DIO - Base de dados: Sample Financials do próprio Power BI:
Link para acessar o relatório ilustrado nas imagens abaixo e interagir com ele: https://app.powerbi.com/view?r=eyJrIjoiOTkyODY4ZWItZWI1Yi00NGE0LTliYTEtZDU0ZDNjMGFlOWZiIiwidCI6IjE1NDRmY2FhLWQ2ZmYtNDU5My04YmJmLWUwMjA3YzIzMGZmZCJ9

* #### Página 01 - Sales Report
  
![Relatorio_Financials](https://github.com/Wandersen99/Power-BI-Analyst/blob/main/Desafio%20de%20Projeto/report_sales.png)
-
* #### Página 02 - Report de Lucro detalhado
  
  ![Relatorio Financials](https://github.com/Wandersen99/Power-BI-Analyst/blob/main/Desafio%20de%20Projeto/Pagina_Report_Lucro.png)
  -



## Projeto de Limpeza e Extração de dados DIO - Base de dados: bd_company.sql disponibilizada pela Juliana Zanelatto

### Informações sobre o projeto:

* O projeto envolveu os seguintes tópicos abaixo:
  
1.Criação de uma instância na Azure para MySQL.

2.Criar o Banco de dados com base disponível no github.

3.Integração do Power BI com MySQL no Azure.

4.Verificar problemas na base a fim de realizar a transformação dos dados.

* As diretrizes para acessar as transformações de dados solicitadas estão neste documento: [Processando e transformando dados com Power BI](https://github.com/Wandersen99/Power-BI-Analyst/blob/main/Projeto/Desafio%20de%20Projeto%20-%20Processando%20e%20Transformando%20Dados%20com%20Power%20BI%20-%20Instru%C3%A7%C3%B5es.docx)


Link para acessar o relatório simples, gerado a partir das informações inseridas na base de dados:

[Relatório Company](https://app.powerbi.com/view?r=eyJrIjoiMTc3MWRiNzEtY2E5Zi00MTYwLWJmNmMtYWYyNDZkYTBjMDlhIiwidCI6IjE1NDRmY2FhLWQ2ZmYtNDU5My04YmJmLWUwMjA3YzIzMGZmZCJ9)

![Relatório criado de bd_company](https://github.com/Wandersen99/Power-BI-Analyst/blob/main/Projeto/relatorio.png)
-
* ### Modelagem realizada: SnowFlake(floco de neve)
![Modelagem do relatório do projeto ETL](https://github.com/Wandersen99/Power-BI-Analyst/blob/main/Projeto/Modelagem.png)
-

* Query SQL usada para extrair os dados solicitados no tratamento do tópico 11: Realize a junção dos colaboradores e respectivos nomes dos gerentes . Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize SQL, especifique no README a query utilizada no processo.

```sql
SELECT 
    concat(e.Fname,' ',e.Lname) AS Gerente, d.Mgr_ssn as Id_Gerente,
    concat(e_colab.Fname, ' ',e_colab.Lname) AS Colaborador, e_colab.ssn as Id_Colaborador
FROM 
    departament d
INNER JOIN 
    employee e ON d.Mgr_ssn = e.ssn
INNER JOIN 
    employee e_colab ON d.Mgr_ssn = e_colab.Super_ssn 
    Where e_colab.ssn != e.Super_ssn;
```

* Resposta do tópico 14 que aborda as diferenças entre usar as opções de mesclar consultas e acrescentar consultas do power bi:
   
 14. Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir.

R: A opção "mesclar consultas" no Power Query é usada quando queremos combinar dados de duas ou mais tabelas com base em uma coluna comum. Ao usar essa opção, podemos especificar uma coluna em cada tabela que contenha informações semelhantes e, em seguida, o Power Query combinará os dados com base nessa coluna.

Por exemplo, se quisermos combinar as tabelas "departament" e "dept_locations" com base na coluna "Dnumber", que representa o número dos departamentos e está presente em ambas as tabelas, podemos usar a opção "mesclar consultas". Isso nos permite juntar as informações de ambas as tabelas com base no relacionamento entre esses números de departamento.

Por outro lado, a opção "acrescentar consultas" é usada quando queremos adicionar linhas de uma tabela a outra tabela existente, desde que ambas as tabelas tenham a mesma estrutura de colunas e tipos de dados. Isso é útil quando temos dados adicionais que desejamos adicionar à tabela existente sem alterar sua estrutura ou conteúdo.

Portanto, no caso descrito, a opção correta seria "mesclar consultas", pois queremos combinar dados com base em uma coluna comum (o número do departamento) em vez de simplesmente adicionar linhas de uma tabela a outra.
-
