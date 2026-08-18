

```SQL
DECLARE @command NVARCHAR(MAX);
SET @command = 'USE [?]; 
                IF EXISTS (SELECT 1 FROM sys.objects WHERE name = ''sp_Processa_Todos_Lancamentos_Hoje'' AND type = ''P'')
                SELECT DB_NAME() AS BancoDeDados, name AS ProcedureName, create_date 
                FROM sys.objects WHERE name = ''sp_Processa_Todos_Lancamentos_Hoje''';

EXEC sp_MSforeachdb @command;
```


