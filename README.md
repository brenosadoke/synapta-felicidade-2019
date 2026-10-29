# Análise do Relatório Mundial de Felicidade 2019

**Candidato:** Breno Sadoque Alves Dias | **Matrícula:** 01695794 | **Período:** 6º (manhã)
**Processo seletivo:** SYNAPTA 2026 (Edital nº 1/2026), Opção 2

## Pergunta da análise
Quais fatores aparecem associados às maiores pontuações de felicidade e quais cuidados devem ser tomados ao interpretar essa relação?

## Dataset e ferramenta
- **Dataset:** World Happiness Report (Kaggle), arquivo `2019.csv`: https://www.kaggle.com/datasets/unsdsn/world-happiness
- **Licença:** CC0: Domínio Público
- **Ferramenta:** Google Sheets (sem Python, então não há dependências; ver `requirements.txt`)

## Como visualizar
- Planilha online (somente leitura): https://docs.google.com/spreadsheets/d/1N40xXfQJmNHwiZCDBUOPX0WMNP_oY_tAaNlvg_6iUNw/edit?usp=sharing
- Ou abra o arquivo `Analise_Felicidade_2019.xlsx` deste repositório.
- Abas: `dados_brutos` (dados originais, sem alterações), `analise` (cálculos) e `top_bottom` (10 mais e 10 menos felizes).
- Para refazer: baixe o `2019.csv` no link acima (veja `data/LEIAME.md`), importe na aba `dados_brutos` e aplique as fórmulas da aba `analise`.

## Colunas utilizadas
| Coluna | Significado |
|---|---|
| Overall rank | Posição do país no ranking (1 = mais feliz) |
| Country or region | Nome do país |
| Score | Nota de felicidade (0 a 10), baseada na avaliação que as pessoas fazem da própria vida |
| GDP per capita | Contribuição da riqueza por pessoa para a nota |
| Social support | Contribuição de ter apoio de alguém em momentos difíceis |
| Healthy life expectancy | Contribuição da expectativa de vida saudável |
| Freedom to make life choices | Contribuição da liberdade para fazer escolhas |

As colunas de fatores não são valores brutos (como renda em reais): indicam o quanto cada fator contribui para a nota do país.

## Limpeza e preparação dos dados
| Verificação | Resultado |
|---|---|
| Países (linhas) | 156 |
| Variáveis (colunas) | 9 |
| Valores ausentes | 0 |
| Países repetidos | 0 (156 únicos) |

| Coluna | Mínimo | Máximo | Zeros |
|---|---|---|---|
| Score | 2,853 | 7,769 | 0 |
| GDP per capita | 0 | 1,684 | 1 |
| Social support | 0 | 1,624 | 1 |
| Healthy life expectancy | 0 | 1,141 | 1 |
| Freedom to make life choices | 0 | 0,631 | 1 |

Todas as notas estão entre 0 e 10 e não há valores negativos. **Decisão:** nenhuma alteração foi feita nos dados. Os zeros foram mantidos, pois são valores possíveis: cada fator é uma contribuição para a nota, e zero indica o nível mais baixo daquele fator.

## Resultados

**Pontuação de felicidade:** média = **5,41** e mediana = **5,38**.
A média soma todas as notas e divide por 156. A mediana é a nota do país do meio quando todos estão em ordem. Como são quase iguais, não há valores extremos puxando a média.

**10 países mais felizes e 10 menos felizes**

| Mais felizes | Menos felizes |
|---|---|
| 1. Finland (7,769) | 147. Haiti (3,597) |
| 2. Denmark (7,600) | 148. Botswana (3,488) |
| 3. Norway (7,554) | 149. Syria (3,462) |
| 4. Iceland (7,494) | 150. Malawi (3,410) |
| 5. Netherlands (7,488) | 151. Yemen (3,380) |
| 6. Switzerland (7,480) | 152. Rwanda (3,334) |
| 7. Sweden (7,343) | 153. Tanzania (3,231) |
| 8. New Zealand (7,307) | 154. Afghanistan (3,203) |
| 9. Canada (7,278) | 155. Central African Republic (3,083) |
| 10. Austria (7,246) | 156. South Sudan (2,853) |

**Correlação com a pontuação de felicidade**

| Fator | Correlação |
|---|---|
| PIB per capita | 0,79 |
| Apoio social | 0,78 |
| Expectativa de vida saudável | 0,78 |
| Liberdade para fazer escolhas | 0,57 |

Quanto mais perto de 1, mais os dois valores sobem juntos.

## Gráficos

![Os 10 países mais felizes em 2019](Os%2010%20pa%C3%ADses%20mais%20felizes%20em%202019.png)
Mostra a nota dos 10 países mais felizes. As barras são parecidas (entre 7,2 e 7,8).

![Os 10 países menos felizes em 2019](Os%2010%20pa%C3%ADses%20menos%20felizes%20em%202019.png)
Mostra a nota dos 10 países menos felizes (entre 2,9 e 3,6), bem abaixo do grupo do topo.

![Relação entre PIB per capita e felicidade](Rela%C3%A7%C3%A3o%20entre%20PIB%20per%20capita%20e%20felicidade%20%282019%29.png)
Cada ponto é um país. Quanto maior a contribuição do PIB, maior tende a ser a nota de felicidade.

![Relação entre expectativa de vida saudável e felicidade](Rela%C3%A7%C3%A3o%20entre%20expectativa%20de%20vida%20saud%C3%A1vel%20e%20felicidade%20%282019%29.png)
Cada ponto é um país. Maior expectativa de vida saudável tende a acompanhar notas mais altas.

## Conclusões
1. A média (5,41) e a mediana (5,38) são quase iguais, então as notas estão distribuídas de forma equilibrada.
2. A diferença entre o país mais feliz (Finland, 7,769) e o menos feliz (South Sudan, 2,853) é de 4,92 pontos.
3. Dentro de cada grupo as notas são parecidas: o Top 10 vai de 7,246 a 7,769 e o Bottom 10 vai de 2,853 a 3,597.
4. PIB (0,79), apoio social (0,78) e expectativa de vida (0,78) têm associação forte com a felicidade, quase do mesmo tamanho.
5. A liberdade tem associação positiva, mas mais fraca (0,57) que os outros três fatores.
6. Nenhum fator explica tudo sozinho: Botswana tem PIB (1,041) acima da média geral (0,905), mas está entre os 10 menos felizes.

## Correlação não é causalidade
Uma correlação alta mostra que dois valores variam juntos, mas não prova que um causa o outro. Países com PIB maior tendem a ser mais felizes, mas isso pode ocorrer porque a riqueza traz felicidade, porque países mais felizes e estáveis produzem mais riqueza, ou porque um terceiro fator influencia os dois. Esta análise não consegue separar essas possibilidades.

## Limitações
- A nota é subjetiva: vem de respostas das pessoas sobre a própria vida.
- Diferenças culturais e métodos de pesquisa podem variar entre países.
- É um retrato de um único ano (2019).
- As colunas de fatores são contribuições para a nota, não medidas diretas.
- Só quatro fatores foram comparados (generosidade e percepção de corrupção ficaram de fora).
- Foi usada apenas correlação simples, sem técnicas estatísticas avançadas.

## Sugestão
Repetir a análise com os anos de 2015 a 2018 do mesmo dataset e incluir generosidade e percepção de corrupção, para ver se os padrões se mantêm.

## Declaração de uso de inteligência artificial generativa
Usei o **Claude (Anthropic)** como guia em todas as etapas: orientação para baixar os dados e montar o repositório, criação das fórmulas do Google Sheets, orientação para os gráficos e escrita deste README. Executei as fórmulas e criei os gráficos na planilha, e os resultados foram conferidos com os dados da aba `dados_brutos`. Li e revisei este texto e consigo explicar cada etapa da análise.
