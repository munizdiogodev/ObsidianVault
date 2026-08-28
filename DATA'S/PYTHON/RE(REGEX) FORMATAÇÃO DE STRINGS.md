[Manipulação de dados desnormalizados em Python: Utilizando re e lstrip() - DEV Community](https://dev.to/womakerscode/manipulacao-de-dados-desnormalizados-em-python-utilizando-re-e-lstrip-221e)



###### Principais Re:
- **`re.search(pattern, string)`**: Procura o padrão em qualquer lugar da string e retorna um objeto de correspondência (_match_) ou `None`.

- **`re.findall(pattern, string)`**: Encontra todas as ocorrências do padrão em uma string e retorna uma lista com os resultados.

- **`re.sub(pattern, repl, string)`**: Substitui as ocorrências do padrão por um novo texto (_repl_) dentro da string.

- **`re.compile(pattern)`**: Compila um padrão de regex em um objeto reutilizável para melhorar a performance em buscas repetidas.

Esse exemplo é bem legal, pois eu precisava caçar os 0800 dentro de um texto com enormes informações, separando entao com o for para vir por cada linha, o regex entra em ação pegando um padrao de como vem o 0800 (0800 880 6976). Coletando então e encontrando todos os casos que tenha esse padrao com o findall

``` PYTHON
  
import re from pypdf import PdfReader

dir = r'C:\Users\diogo.souza\Downloads\TOP THERM - 28.08.pdf'
pdf_reader = PdfReader(dir)
text_target = '0800'

# [\s\.-]? = depois do 0800 pode estar vazio ou ter um hifen
# \d{3} = ter 3 digitos 


padrao_0800 = r'0800[\s\.-]?\d{3}[\s\.-]?\d{4}'

  
coletar_conteudo= []


len_pages = len(pdf_reader.pages)

for paginas in range(len_pages):

    page = pdf_reader.pages[paginas]

    text = page.extract_text()

    encontrado = re.findall(padrao_0800,text)

    if encontrado:

        coletar_conteudo.extend(encontrado)

print(coletar_conteudo)
```