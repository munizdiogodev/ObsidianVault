Lembrando que o arquivo .csv deve estar na mesma rede que esta hospedado o servidor SQL

``` SQL
USE MailingDB;
GO

-- Garante que o SQL leia as datas como Ano-Mês-Dia
SET DATEFORMAT ymd;

BULK INSERT dbo.lemit
FROM '\\10.0.0.20\mis\1249876-NORMAL_2025.csv'
WITH (
    FIRSTROW = 2,                  -- Pula a linha do cabeçalho do CSV
    FIELDTERMINATOR = ';',         -- Delimitador de colunas (ponto e vírgula)
    ROWTERMINATOR = '\n',          -- Quebra de linha
    CODEPAGE = 'ACP',              -- Codificação ANSI/Windows para os acentos virem certos
    KEEPNULLS,                     -- Mantém campos vazios como NULL em vez de dar erro
    TABLOCK                        -- Bloqueia a tabela durante o insert para máxima performance

);

GO
```