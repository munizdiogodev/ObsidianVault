``` python
df_share = df_prod.join(df_regiao,on="GRANDE REGIÃO",how="inner")
```

Basicamente o inner join no banco, porém com a sintaxe mais diferente:

```python
variavel = tabela1.join(tabela2,on="COLUNA IGUAL",how="modo de juntar")
```
