
Podemos alem de colocar na cara as credenciais no código bruto, termos um arquivo env para guarda-los e chamar essas credenciais de forma ofuscada, segue exemplo: 


criamos um arquivo .env no ambiente no vscode, senod:


```env
TOPTHERM_EMAIL = 'diogo.souza@toptherm.com.br'

TOPTHERM_SENHA = 'mudar123'
```


e então dentro do nosso código bruto, instanciamos dessa maneira:

``` python
import os

from pathlib import Path

from dotenv import load_dotenv

from playwright.sync_api import sync_playwright

  

# Localizando e carregando o .env

caminho_env = Path(__file__).resolve().parent / ".env"

load_dotenv(caminho_env)

  

email = os.getenv("TOPTHERM_EMAIL")

senha = os.getenv("TOPTHERM_SENHA")

  

URL_LOGIN = "https://toptherm.lh.com.br:9060/sso/login"

  

# Verificando se as credenciais existem
.

if not email or not senha:

    raise ValueError("Configure o e-mail e a senha no arquivo .env")

```