# Dashboard Power BI — cinco páginas

Este documento descreve o dashboard final aprovado, representado nas cinco screenshots abaixo e no projeto PBIP/PBIR versionado. O canvas permanece em 1920 × 1080.

O [PBIX final](dashboard_ctps_2020_2022.pbix) e o [projeto PBIP](CTPS.pbip) contêm as cinco páginas na ordem apresentada abaixo. As definições de relatório e os recursos incorporados no PBIX correspondem ao PBIR versionado em `CTPS.Report/`. O PBIP referencia `CTPS.SemanticModel/`, cujas definições foram copiadas sem alterações.

## Páginas e finalidade

| Página | Finalidade | Interação e contexto |
|---|---|---|
| [1. Visão Geral](01_visao_geral.png) | Apresentar volume, concentração temporal, Top 5 UFs, protocolo em barra 100% e evolução mensal | Filtros Período, Protocolo e UF do órgão; destaques documentais identificados |
| [2. Perfil dos Registros](02_perfil_registros.png) | Explorar Escolaridade Top 8, raça/cor, sexo em barra 100% e cidadania | Os mesmos três filtros; faixa de perfil predominante fixa para 2020–2022 |
| [3. Qualidade dos Dados](03_qualidade_dados.png) | Mostrar integridade, rastreabilidade, recorte analítico e limites de interpretação | Base completa preservada; sem filtros operantes |
| [4. Síntese Analítica](04_sintese_analitica.png) | Reunir os achados temporais, regionais, de protocolo e de perfil com ressalvas metodológicas | Conteúdo fixo/documental de 2020–2022; sem filtros operantes |
| [5. Recomendações Executivas](05_recomendacoes_executivas.png) | Traduzir os achados em prioridades de uso, monitoramento e aprofundamento | Conteúdo fixo/documental baseado em 2020–2022; sem filtros operantes |

## Base completa e recorte analítico

A fonte mantém **485.430 registros**. Um deles tem `Data CTPS Gerada = 2023-01` no arquivo oficial `dados_ctps_2022.xlsx`, com protocolo e emissão em dezembro de 2022. Ele permanece na base e fica fora apenas das análises de 2020–2022, que abrangem **485.429 registros**.

| Indicador | Base completa preservada | Recorte 2020–2022 |
|---|---:|---:|
| Registros | 485.430 | 485.429 |
| 1ª via | 351.527 | 351.527 |
| 2ª via | 133.903 | 133.902 |

Os insights, as tabelas analíticas do pipeline e as consultas SQL deste repositório usam o recorte 2020–2022. Os controles de qualidade e a contagem de repetições usam a base completa; nenhuma linha foi removida da base processada.

## Filtros e referências fixas

- **Visão Geral e Perfil:** o PBIR apresenta segmentadores de Período (`Calendario.Ano`), Protocolo e UF do órgão, com 2020, 2021 e 2022 selecionados. Gráficos e indicadores exploratórios usam as medidas existentes; Escolaridade mantém Top 8 e o ranking regional, Top 5.
- **Destaques documentais:** a concentração de 96,9%, os totais anuais de 470.560, 11.707 e 3.162, o Top 5 de 61,6% e a faixa de perfil predominante são referências do período completo. Não devem ser interpretados como resultados dinâmicos de seleções.
- **Qualidade:** o PBIR não contém segmentadores, filtros de página ou filtros de visual; não foram encontrados grupos de sincronização. Os quatro indicadores continuam vinculados às medidas existentes: 485.430 processados, 0 removidos, 0 datas inválidas e 1 fora do período. A página não oferece filtragem exploratória.
- **Síntese e Recomendações:** o PBIR contém somente textos e formas, sem consultas de dados ou segmentadores. A ausência de filtros operantes e a natureza fixa são intencionais: o conteúdo não se recalcula quando dados ou seleções mudam.

## Qualidade e rastreabilidade

As **25.844 ocorrências repetidas** são linhas excedentes após a primeira ocorrência de cada combinação das 18 colunas de negócio, preservadas na base completa. Não representam duplicatas confirmadas, pessoas ou combinações únicas. Sem identificador individual, recorrências não são removidas automaticamente.

Os **12 registros com UF original IG** permanecem com a categoria da fonte. O fluxo documentado é: **5 XLSX oficiais → manifesto com URL, tamanho e SHA-256 → Python/pandas → CSV + SQLite → SQL → Power BI**. Esquema, datas e quantidade de registros são validados no processamento.

## Síntese e recomendações

A Síntese apresenta **96,9%** de concentração temporal, **61,6%** regional, **72,4%** de predominância da 1ª via e **62,6%** para Pardo, principal categoria de raça/cor declarada. Os textos descrevem registros e os limites de cobertura da publicação.

Recomendações Executivas organiza três prioridades P1 — comparação temporal, continuidade da publicação e controles de qualidade — e duas P2 — contextualização territorial e enriquecimento analítico antes de conclusões sobre mercado de trabalho. São prioridades de uso e investigação dos dados, não recomendações de política pública.

O fechamento destaca que a qualidade da decisão depende da cobertura, semântica e confiabilidade da fonte. Emissões de CTPS não medem pessoas únicas, emprego, contratação, desemprego ou formalização, nem sustentam causalidade econômica. UF corresponde ao órgão emissor, não necessariamente à residência.

## Referências técnicas

[modelo.md](modelo.md), [medidas.dax](medidas.dax) e [PowerQuery.m](PowerQuery.m) são referências de apoio. Esta atualização é exclusivamente documental; não altera o modelo validado, suas consultas ou cálculos.
