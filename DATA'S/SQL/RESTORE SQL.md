
```SQL
USE [master];
GO

-- 1. Força a queda de conexões no banco CEP_07
ALTER DATABASE [CEP_07] SET SINGLE_USER WITH ROLLBACK IMMEDIATE;
GO

-- 2. Executa a restauração usando os caminhos do servidor
RESTORE DATABASE [CEP_07]
FROM DISK = 'D:\MSSQL\MIS\CEP_2026_01_01.bak' 
WITH REPLACE,
MOVE 'CEP_2026_01_01'     TO 'D:\MSSQL\DATA\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\CEP_07.mdf', 
MOVE 'CEP_2026_01_01_log' TO 'D:\MSSQL\DATA\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\CEP_07_log.ldf',
STATS = 5;
GO

-- 3. Retorna o banco para acesso múltiplo
ALTER DATABASE [CEP_07] SET MULTI_USER;
GO
```

use isso para saber o nome do logical de onde esta
```sql

RESTORE FILELISTONLY 
FROM DISK = 'D:\MSSQL\MIS\CEP_2026_07_02.bak';

```




.mdf (master data file) e a estrutura do banco em todo, tabelas, views, procedures e etc, tudo mesmo

.ldf (log data file) registra apenas os registros das ocorrencias do mdf


NAO ESQUECER DE DAR PEMISSAO NO CEP

fica em segurança-logons :

![[Pasted image 20260804101440.png]]
