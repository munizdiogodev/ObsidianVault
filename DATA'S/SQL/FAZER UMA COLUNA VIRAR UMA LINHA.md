

 Nesse contexto, usei o FOR XML para trazer na mesma linha os ultimos 3 produtos do cliente, ligando entao pela cdcli do pedsai 1 com a pedsai 2



```SQL
SELECT
W1.CdCli,
W1.Produtos_Concatenados
FROM

(
SELECT 
    p1.CdCli,
    STUFF((
        SELECT TOP 3 ' / ' + pd.DescPrd
        FROM VANROOY.dbo.PedSai p2
        INNER JOIN VANROOY.dbo.It_ped ipd ON ipd.NrContrPed = p2.NrContrPed
        INNER JOIN VANROOY.dbo.Produto pd ON pd.CdPrd = ipd.CdPrd
		INNER JOIN VANROOY.dbo.ProdutoComposicao pc on pc.CdPrd = ipd.CdPrd
		AND Pd.DescPrd NOT LIKE ('%BRINDE%')
        WHERE p2.CdCli = p1.CdCli
        FOR XML PATH(''), TYPE).value('.', 'NVARCHAR(MAX)'), 1, 3, '') AS Produtos_Concatenados
FROM 
    VANROOY.dbo.PedSai p1
WHERE 
    p1.CdCli IN ('0005689637'
,'0005674182'
,'0005666481'
```


