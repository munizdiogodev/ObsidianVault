[pandas GroupBy: Your Guide to Grouping Data in Python – Real Python](https://realpython.com/pandas-groupby/#the-hello-world-of-pandas-groupby)

Acima é a url do site que usei tanto para entender quanto pra aplicar

vejamos que na época o "Unnamed: 9" é uma coluna a qual quero agrupar o conteudo e saber quantas vezes ele mesmo aparece ()

``` python

grade_group = df.groupby("Unnamed: 9", as_index=True)["Unnamed: 9"].count()



```

``` python
8007700147     1
8007702901     6
8007706972    25
8007706973    67
8007706974    30
8007706975    39
8007706976    57
8007706978    66
8007706980     2
8007706981    54
8007706982    30
```

Ficando basicamente assim