
```SQL
SELECT 
    t.name AS Tabela,
    c.name AS Coluna,
    ty.name AS Tipo_Dado,
    c.max_length AS Tamanho_Maximo
FROM sys.columns c
JOIN sys.tables t ON c.object_id = t.object_id
JOIN sys.types ty ON c.user_type_id = ty.user_type_id
WHERE c.name LIKE '%CdPrd%' -- Substitua pelo nome da coluna que deseja achar
ORDER BY t.name;
```


