
```SQL
SELECT DISTINCT 
    OBJECT_NAME(sm.object_id) AS Nome_Procedure
FROM sys.sql_modules sm
JOIN sys.objects o ON o.object_id = sm.object_id
WHERE sm.definition LIKE '%lancamentos%' -- Substitua pelo nome da sua tabela
  AND o.type = 'P'; -- Filtra apenas por Stored Procedures
```