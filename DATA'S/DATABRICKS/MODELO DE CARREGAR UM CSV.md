Exemplo de criação da view de um csv, esse pathfile é um exemplo
``` python
# Caminho completo do arquivo no seu Volume
from pyspark.sql.functions import *
from pyspark.sql.types import *
path_file = "/Volumes/workspace/sandbox/mundo_transfermarkt_competicoes_brasileirao_serie_a/mundo_transfermarkt_competicoes_brasileirao_serie_a.csv"

  

# Lendo o CSV com as opções corretas (separador, cabeçalho e encoding para evitar bugs em acentos)

df = spark.read.format("csv") \

.option("header", "true") \

.option("inferSchema", "true") \

.option("sep", ",") \

.option("encoding", "ISO-8859-1") \

.load(path_file)

  

# Exibindo os dados

df.display()