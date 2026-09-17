
``` PYTHON
 .withColumn("MES GER", concat_ws("-",col("ANO"), col("MÊS"),col("MES_NUMERICO"))).display()
```

Obs: Basta colocar o sinal no primeiro parametro, de resto vao ser as colunas

