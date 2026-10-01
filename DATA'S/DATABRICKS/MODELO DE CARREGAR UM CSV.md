
``` python
df = spark.read.format("csv")\

    .option("header","true")\

    .option("inferSchema","true")\

    .option("sep",";")\

    .option("encoding","ISO-8859-1")\

    .load(path_file)
```