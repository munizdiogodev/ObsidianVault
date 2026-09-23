
Nesse contexto, eu precisava achar um telefone de uma coluna da tabelaX que pode estar em um varias colunas da tabelaY

```SQL
select distinct

l.DT_CHAMADA,
l.NR_TELEFONE,
telEncontrado
from
LHTEC.dbo.TB_LIGACOES_LH_URA l

--basicamente fazendo um inner join seco (entao só vai trazer os telefones que estao de fato em um das colunas da outra tabela)
inner join MailingDB.dbo.mailing_v2 cli

--mete um cross apply pra ele trazer no seco
cross apply(

--coloca no values todas as colunas que podem ser encontrados o telefone
values

(cli.tel1),  
(cli.tel2),(cli.tel3),  (cli.tel4),  (cli.tel5),
(cli.tel6),  (cli.tel7),  (cli.tel8),  (cli.tel9),  (cli.tel10),
(cli.tel11), (cli.tel12), (cli.tel13), (cli.tel14), (cli.tel15),
(cli.tel16), (cli.tel17), (cli.tel18), (cli.tel19), (cli.tel20)

) as t(telEncontrado) --criando entao uma coluna só, de um nome para ela
on l.NR_TELEFONE = telEncontrado


where l.TX_STATUS = 'Abandono na saudacao'
and l.DT_CHAMADA <= GETDATE() - 5
```