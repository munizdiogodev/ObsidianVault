
Podemos alem de colocar na cara as credenciais no código bruto, termos um arquivo env para guarda-los e chamar essas credenciais de forma ofuscada, segue exemplo: 


criamos um arquivo .env no ambiente no vscode, senod:


```env
TOPTHERM_EMAIL = 'diogo.souza@toptherm.com.br'

TOPTHERM_SENHA = 'mudar123'
```


e então dentro do nosso código bruto, instanciamos dessa maneira:
