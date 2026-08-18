``` SQL

MERGE db_midia.dbo.lancamentos as m --TABELA TARGET
USING dados as d --TABELA SOURCE
ON
convert(date,d.data_hora) = convert(date,m.data_hora)
and d.id_crm = m.id_crm
and d.id_midia = m.id_midia
-- O QUE IRÁ COMBINAR AS LINHAS DA SOURCE E TARGET PARA QUE ACONTEÇA O MATCHED OU O NOT MATCHED

WHEN MATCHED THEN --QUANDO COMBINAR AS LINHA DA TABELA TARGET, COM A SOURCE

	update set 
		m.ligacoes = d.ligacoes,
		m.ocorrencias = d.ocorrencias,
		m.ligacoes_dia = d.ligacoes_dia,
		m.vlr_midia = d.vlr_midia
		
		
WHEN NOT MATCHED BY TARGET THEN 
--QUANDO **NÃO** COMBINAR AS LINHA DA TABELA TARGET, COM A SOURCE

	insert (id_crm,	descricao,	emissora,	programa,	produto,	vlr_midia,	vlr_cache,	data_hora,	ligacoes,	observacoes,	id_midia,	ocorrencias,	veiculo,	tipo,	interact_id,	interact_descricao,	ligacoes_dia,	agencia,	nivel,	assistido)
	values (d.id_crm, d.descricao,	d.emissora,	d.programa,	d.produto,	d.vlr_midia,	d.vlr_cache,	d.data_hora,	d.ligacoes,	d.observacoes,	d.id_midia,	d.ocorrencias,	d.veiculo,	d.tipo,	d.interact_id,	d.interact_descricao,	d.ligacoes_dia,	d.agencia,	d.nivel,d.assistido)
	;
```