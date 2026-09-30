Bom, nesse contexto eu precisava ter 2 for i, porem combinando os indices de cada um deles, ex:

```python
for codeC, codeM in zip(lista_cd_Campanha, lista_cd_mailing):
```
Nesse exemplo, eu precisava do codeC (código do Mailing) e codeM(codigo da Campanha) no mesmos indices, ou seja:

Indice 0 do codeC 
Indice 0 do codeM


Indice 1 do codeC
Indice 1 do codeM

e por assim adiante...


Pergunta: Por qual motivo eu nao fiz for dentro de for?
Ex:
```python
For codeC in lista_cd_Campanha:
	for codeM in lista_cd_mailing:

```

Simples! se eu fizesse dessa maneira, eu iria combinar todos os tipos de indices do codeC com o codeM

ou seja:

Indice 0 do codeC 
Indice 0 do codeM

Indice 0 do codeC
Indice 1 do codeM

Indice 0 do codeC
Indice 2 do codeM


E por assim vai até combinar todos...