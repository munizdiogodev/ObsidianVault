```python
df.withColumn("VENDAS", regexp_replace(col("VENDAS"), ",", ".")).display()
```