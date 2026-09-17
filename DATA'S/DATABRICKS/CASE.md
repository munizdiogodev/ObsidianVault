```PYTHON
df.withColumn("MES_NUMERICO",

    when(col("MÊS")=="JAN",1)

    .when(col("MÊS")=="FEV",2)

    .when(col("MÊS")=="ABR",4)

    .when(col("MÊS")=="MAI",5)

    .when(col("MÊS")=="JUN",6)

    .when(col("MÊS")=="JUL",7)

    .when(col("MÊS")=="AGO",8)

    .when(col("MÊS")=="SET",9)

    .when(col("MÊS")=="OUT",10)

    .when(col("MÊS")=="NOV",11)

    .when(col("MÊS")=="DEZ",12)

    .when(col("MÊS")=="MAR",3)

    .otherwise(0)).display()
```