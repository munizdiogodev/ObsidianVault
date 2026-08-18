

```SQL
-- Multiplicamos por 100.0 para transformar em decimal e depois formatamos
CAST( ((w1.CHAMADAS_LONGAS * 100.0) / w1.TOTAL_DISCAGEM) AS DECIMAL(10,2)) AS PERC
```

