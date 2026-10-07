# Modelo Power BI — referência técnica

Este documento preserva as orientações iniciais de implementação do modelo, Power Query e DAX como referência técnica. O [PBIX final](dashboard_ctps_2020_2022.pbix) e o [PBIP](CTPS.pbip) representam o relatório aprovado de cinco páginas, descrito em [`dashboard_spec.md`](dashboard_spec.md). O projeto editável referencia as definições originais em `CTPS.SemanticModel/`, copiadas sem alterações; não é necessário reconstruir o modelo validado.

No Desktop, crie o parâmetro de texto `CaminhoCSV` apontando para o CSV processado e importe `PowerQuery.m` como a consulta `ctps_emissoes`. As datas convertidas usam o dia 1 como representação técnica do mês, sem precisão diária. Crie cada medida de `medidas.dax` separadamente; formate a participação como percentual. Esses arquivos de apoio são referências de implementação, não substitutos das definições finais do modelo.

Sem filtros, os cartões devem mostrar 485.430 registros, 351.527 de primeira via e 133.903 de segunda via. A medida `Repeticoes de registros` conta as linhas excedentes após a primeira ocorrência de cada combinação das 18 colunas de negócio, como o relatório Python: 25.844 sem filtros. Não conta pessoas nem combinações únicas. `registro_id` é um hash de atributos, não uma chave única de atendimento.

`ctps_emissoes` tem uma linha para cada registro publicado nos arquivos oficiais. O modelo não afirma que cada linha represente uma pessoa única.

Para a primeira versão, a tabela fato é `ctps_emissoes`. As dimensões podem ser derivadas no Power Query ou no modelo: `DimPeriodo` (período, ano e mês), `DimUF` (UF e município do órgão), `DimProtocolo` e `DimPerfil` (sexo, escolaridade, raça/cor, estado civil e cidadania).

Use relações unidirecionais de dimensões para a fato e medidas explícitas em DAX. A escolha segue a orientação oficial sobre modelo em estrela: [Microsoft Learn](https://learn.microsoft.com/power-bi/guidance/star-schema).

As cinco páginas atuais estão detalhadas em [`dashboard_spec.md`](dashboard_spec.md): Visão Geral, Perfil dos Registros, Qualidade dos Dados, Síntese Analítica e Recomendações Executivas. O painel deve deixar claro que os números descrevem a publicação administrativa, não contratação ou impacto causal.

Para inspecionar os dados já importados sem refresh, use o PBIX final. O PBIP versiona as definições do relatório e do modelo; caches e configurações locais de sessão não são distribuídos. Esta consolidação não alterou origens, relações, medidas ou cálculos.
