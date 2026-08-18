
Nesse meu contexto, precisei pegar clientes que compraram em 2026, e sua primeira compra na TOP, pra isso tive que usar o CROSS APPLY pra trazer a primeira compra do indivíduo.

Então basicamente CROSS APPLY funciona como um inner join, porém voce fazendo uma seleção de filtro pré para que voce possar associar cada linha para cada resultado do cross apply.


``` sql


-- CROSS APPLY: Descarta o cliente se a subquery retornar vazio
SELECT c.CdCli, c.Nome, p.DtPed
FROM Clientes c
CROSS APPLY (
    SELECT TOP 1 sub.DtPed 
    FROM Pedidos sub 
    WHERE sub.CdCli = c.CdCli 
    ORDER BY sub.DtPed DESC
) p;




--  OUTER APPLY: Mantém o cliente mesmo se a subquery retornar vazio (traz NULL)
SELECT c.CdCli, c.Nome, p.DtPed
FROM Clientes c
OUTER APPLY (
    SELECT TOP 1 sub.DtPed 
    FROM Pedidos sub 
    WHERE sub.CdCli = c.CdCli 
    ORDER BY sub.DtPed DESC
) p;
```


OBS:
CROSS APPLY - INNER JOIN, DESCARTANDO O QUE RETORNA VAZIO

OUTER APPLY  - LEFT JOIN, MANTEM MESMO SE A SUBQUERY RETORNAR VAZIO

