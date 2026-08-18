

*PIVOT*

transformar linhas, muito bom para quando queremos fazer com que varias linhas com o mesmo sentido (mes, nome e etc) vire coluna.




Essa é a tabela principal a qual ira fazer o pivô (exemplo do youtube) -> [Transformando linhas em colunas com o operador PIVOT | SQL](https://www.youtube.com/watch?v=DIVqHeecym4)

![[Pasted image 20260220104622.png]]



 
Aqui o exemplo, vejamos que aparece o mesmo vendedor, o mesmo mes e o mesmo ano, fazendo com que facilmente possa ser fundido para um unico tópico [VENDEDOR|MES|ANO] <- as colunas

![[Pasted image 20260220102638.png]]



Alguns tópicos do pivot para entendermos de maneira mais fácil.

![[Pasted image 20260220105003.png]]

1- Criando um CTE para a tabela de origem, e a tabela de pivot.

Sabendo que a VENDA_LIQUIDA é a coluna que devemos somar para criar uma nova coluna.
fazendo isso por mes (FOR MES IN)

OBS: SABENDO QUE DEVE DEIXAR NO MESMO INDICE AS COLUNAS



*UNPIVOT*
	basta entender


```sql
select
cpf,
codigo,
numero_telefone,
origem_telefone
from

(select top 22
v.cpf,
v.codigo,
v.tel1,
v.tel2,
v.tel3


from
MailingDB.dbo.mailing_v2 v
) as fonte

UNPIVOT(
	numero_telefone for origem_telefone in 
	(tel1, tel2, tel3) 
)AS tabelaunpivot
where numero_telefone is not null;
```

![[Pasted image 20260318135447.png]]