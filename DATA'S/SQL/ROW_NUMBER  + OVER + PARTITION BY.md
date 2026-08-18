
Podemos usar o row  number + over + partition by para rankear elementos por algum parametro

```SQL

ROW_NUMBER () over(partition by p.NrPed order by h.DtContato desc) as linha

```

nesse caso acima, estamos rankeando a coluna nrped por data de contanto, ficando algo como:


```excel

 
|Nrped|DtContato|rank|
|412412|15/06/2026|1|
|412412|15/03/2026|2|
|412412|12/01/2026|3|

```




TAMBÉM PODEMOS USAR SÓ PRA CONTAR LINHAS

```SQL
'A' + CONVERT(vARCHAR(15), @IdProdutoComposicao + ROW_NUMBER() over(order by (SELECT NULL)))


-- O SELECT NULL FAZ ISSO, deixando com que o parametro nao fique vazio e ele conte por linha
```