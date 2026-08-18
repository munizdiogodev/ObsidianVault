O Database Mail (Correio Eletrônico do Banco de Dados) é um recurso do SQL Server que permite enviar mensagens de e-mail a partir do Engine do Banco de Dados. Para que ele funcione, são necessárias três entidades configuradas em sequência: o **Servidor SMTP**, a **Conta**, e o **Perfil**.



![[Pasted image 20251202164047.png]]



Para conseguirmos mandar email atraves do SQL, precisamos de algumas seguintes diretrizes para funcionar de maneira correta:


- Servidor SMTP  = o seu ambiente precisara de um SMTP, o protocolo de saída que enviara mensagem para fora
- Conta de Email = Login e senha, além de vc possuir seu email corporativo, precisa-se criar um login e senha propriamente para a conta SQL.

1- Criação de conta 
```SQL
EXECUTE msdb.dbo.sysmail_add_account_sp

@account_name = 'Conta_Robo_Wpp',        -- Nome interno da conta para referência no perfil.

@email_address = 'robo01@toptherm.com.br', -- Endereço de e-mail que aparecerá como remetente.

@display_name = 'Robô de Relatórios - WPP',  -- Nome de exibição amigável para o destinatário.

    -- **** INFORMAÇÃO CRÍTICA A SER VALIDADA COM TI ****

@mailserver_name = 'smtp.toptherm.com.br',  -- Exemplo: Servidor SMTP do Outlook 
    
-- O endereço CORRETO deve ser fornecido pela sua TI (ex: smtp.suaempresa.local).

@port = 587, -- Porta padrão para SMTP seguro (TLS).

@username = 'robo01@toptherm.com.br', -- Login para autenticação no servidor SMTP.

@password = 'SenhaDoRobo01Aqui';-- Senha REAL da caixa postal 'robo01'.

-- ** IMPORTANTE: Se o seu SMTP exigir SSL/TLS, você DEVE adicionar os seguintes parâmetros:**

-- ,@enable_ssl = 1

-- Caso contrário, o envio pode falhar.
```


2 - Criação de Perfil que usara dos emails/conta
```SQL
EXECUTE msdb.dbo.sysmail_add_profile_sp

    @profile_name = 'robo01', -- O nome do Perfil. É o "apelido" que você usa no parâmetro @profile_name ao enviar o e-mail.

    @description = 'Perfil para envio de relatórios automatizados de WhatsApp'; -- Uma breve descrição do perfil para fins de documentação interna.
```



3 - O passo final é linkar a conta (1) com o perfil (2)

```SQL
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp
    @profile_name = 'robo01',
    @account_name = 'Conta_Robo_Wpp',
    @sequence_number = 1; -- Ordem de uso (útil se houver mais de uma conta)

```



4 - Teste para execução
``` sql
-- 1. DECLARAÇÃO DE VARIÁVEIS (Obrigatório para o assunto)

DECLARE @body NVARCHAR(MAX);

DECLARE @assunto_email NVARCHAR(255);
-- (Assumindo que @body foi preenchido por uma consulta)

-- 2. CALCULA O ASSUNTO

SET @assunto_email = 'Whatsapp por Operador : ' + CONVERT(NVARCHAR, GETDATE()-1, 103);

-- 3. EXECUTA O ENVIO

EXEC msdb.dbo.sp_send_dbmail

    @body = @body,

    @recipients = 'diogo.souza@toptherm.com.br',

    @subject = @assunto_email, -- Parâmetro que usa o Perfil

    @profile_name = 'robo01', -- O NOME DO PERFIL

    @body_format = 'HTML';
```


Depois disso podemos prosseguir [[LAYOUT EMAIL - SQL]]