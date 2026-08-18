Bom, o meu problema para essa anotação foi tentar localizar se em um indice especifico tinha o número 9 ou não, pois eu queria saber para aplicar outra lógica por cima, dai que podemos falar sobre o substring:

Tem sua principal função localizar uma string a partir de do indice 
```SQL
SUBSTRING(w1.destino,5,1)
--o primeiro parametro é a sua string localizada,
--o segundo parametro é a partir de qual indice voce quer começar a especificar o que voce quer ser mostrado
--o terceiro parametro é o que quantos caracteres voce quer que apareça
```


ex:



```SQL
SUBSTRING(w1.destino,5,1) as test
--557181676048 -> 8
--558596442706 -> 9
```

ou seja, retornado a caractere a partir do indice de começo e localização.