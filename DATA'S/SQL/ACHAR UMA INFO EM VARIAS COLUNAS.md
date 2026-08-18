krai tem como achar um telefone em varias colunas desse jeito ai ó pique efeito reverso: 
```SQL
SELECT * 
FROM MailingDB.DBO.mailing_v2 C WITH(NOLOCK)
WHERE '11964445563' IN (
    C.tel1,  C.tel2,  C.tel3,  C.tel4,  C.tel5, 
    C.tel6,  C.tel7,  C.tel8,  C.tel9,  C.tel10, 
    C.tel11, C.tel12, C.tel13, C.tel14, C.tel15, 
    C.tel16, C.tel17, C.tel18, C.tel19, C.tel20
);


```