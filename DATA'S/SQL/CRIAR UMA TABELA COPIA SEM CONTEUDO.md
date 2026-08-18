


```SQL
SELECT * 

INTO 

LHTEC.dbo.TOPTHERM_FUNC_LHTEC -- TABELA NOVA 

FROM dbo.TOPTHERM_FUNC_LHTEC_2 -- TABELA ANTIGA

WHERE 1 = 0; -- A mágica está aqui: impede que os dados sejam copiados


```