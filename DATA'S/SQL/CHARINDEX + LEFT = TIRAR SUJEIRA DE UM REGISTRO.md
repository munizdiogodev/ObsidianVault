
**Objetivo:** Extrair apenas o primeiro nome de uma string que contém um padrão de separador (Ex: `NOME - DATA`).

### 1. A Função `CHARINDEX` (O Localizador)

Imagine que o `CHARINDEX` é um sensor. Ele varre o texto da esquerda para a direita procurando um caractere específico (o nosso alvo).

- **O que ele faz:** Retorna a **posição numérica** (o índice) de onde o alvo está.
    
- **Exemplo:** Em `PAMELA - RH`, o traço `-` está na posição **8**.
    

### 2. A Função `LEFT` (A Tesoura)

O `LEFT` corta o texto começando do início (esquerda) até o número de caracteres que você mandar.

- **O problema:** Se você mandar ele cortar até a posição do `CHARINDEX` (8), ele trará o traço junto: `PAMELA -`.
    
- **A solução:** Usamos o **`- 1`**.
    

### 3. A Lógica do `- 1` (O Ajuste Fino)

O `- 1` é o que garante que a tesoura pare **uma casa antes** do alvo.

**Exemplo prático:**

> **Texto:** `DIOGO - TOP`
> 
> 1. `CHARINDEX` encontra o `-` na posição **7**.
>     
> 2. Fazemos a conta: `7 - 1 = 6`.
>     
> 3. O `LEFT` corta os **6** primeiros caracteres.
>     
> 4. **Resultado:** `DIOGO`



```sql
CASE 
    -- 1. Verifica se o alvo (traço) existe na string
    WHEN CHARINDEX('-', f.NmFunc) > 0 
    
    -- 2. Se existe, corta até a posição dele, menos um caractere
    THEN LEFT(f.NmFunc, CHARINDEX('-', f.NmFunc) - 1)
    
    -- 3. Se não existe traço, mantém o nome como está (segurança)
    ELSE f.NmFunc 
END
```