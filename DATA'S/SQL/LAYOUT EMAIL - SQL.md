depois que [[MANDAR E-MAIL PELO SQL]] for concluído, podemos criar um layout para ficar mais visual no e-mail:

aqui há um modelo bem básico para se usar, apenas para ter ideia de como funciona:

``` SQL


USE LHTEC;


GO

DECLARE @body NVARCHAR(MAX) = '';
DECLARE @assunto_email NVARCHAR(255);



SET @assunto_email = 'Whatsapp por Operador : ' + CONVERT(NVARCHAR, GETDATE() - 1, 103);
-- Estilo para centralizar o conteúdo da célula de dados e cabeçalhos
DECLARE @data_cell_style NVARCHAR(100) = ' style="padding: 4px 10px; text-align: center;"';

-- Otimizações:
-- 1. Removido width='100%' para que a tabela ocupe apenas o espaço necessário.
-- 2. Adicionada uma tag <div> externa para centralizar a tabela na largura do email.
SET @body =
'<div style="width: 100%; text-align: center;">' -- Div para centralizar a tabela
+ '<table border=1 style="border:1px solid black; border-collapse: collapse; margin: 0 auto; min-width: 300px;">' -- Removido width='100%', adicionado margin e min-width
+ '<tr><th colspan=''2'' bgcolor=''#ADD8E6'' style="padding: 8px; text-align: center;">' -- Cor azul claro para o cabeçalho
+ '<h3>Leads Whatsapp por Operador</h3></th></tr>'
+ '<tr bgcolor=''#A9A9A9'' style="color: white;">' -- Cor cinza escuro para cabeçalho da coluna
+ '<th style="padding: 6px 12px; text-align: center;">Vendedor</th>'
+ '<th style="padding: 6px 12px; text-align: center;">Leads</th>'
+ '</tr>'
+ CAST(
(
    SELECT
        VENDEDOR [td],
        LEADS [td]
    FROM [dbo].[VW_LEADS_WPP_P_OPERADOR]
    FOR XML RAW('tr'), ELEMENTS
) AS NVARCHAR(MAX))
-- Injetando o style para centralizar e ajustar o padding em todas as <td> geradas
+ REPLACE(REPLACE(@body, '<td', '<td' + @data_cell_style), '</tr>', '</tr>' + CHAR(13))
+ '<tr><td colspan=''2'' bgcolor=''#A9A9A9'' style="color: white; padding: 6px; text-align: center;">' -- Cor cinza escuro para rodapé
+ 'Leads do dia: ' + CONVERT(NVARCHAR, GETDATE()-1, 103)
+ '</td></tr></table>'
+ '</div>';



EXEC msdb.dbo.sp_send_dbmail
    @body = @body,
    @recipients = 'diogo.souza@toptherm.com.br',
    @subject = @assunto_email,
    @profile_name = 'robo01',
    @body_format = 'HTML';


GO
```




Visualmente no E-mail:
![[Pasted image 20251202173456.png]]