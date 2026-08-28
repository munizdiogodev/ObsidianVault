[Manipulação de dados desnormalizados em Python: Utilizando re e lstrip() - DEV Community](https://dev.to/womakerscode/manipulacao-de-dados-desnormalizados-em-python-utilizando-re-e-lstrip-221e)

Esse exemplo é bem legal, pois eu precisava caçar os 0800 dentro de um texto com enormes informações, separando entao com o for para vir por cada linha, o regex entra em ação pegando apenas nume
``` PYTHON
  
import re from pypdf import PdfReader

dir = r'C:\Users\diogo.souza\Downloads\TOP THERM - 28.08.pdf'
pdf_reader = PdfReader(dir)
text_target = '0800'


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