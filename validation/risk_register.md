# Registro de riscos — validação de mercado e mensagem

**Escopo:** riscos conhecidos antes de build/publicação.
**Escala qualitativa:** Alto / Médio / Baixo. Não representa probabilidade estatística.

| ID | Tipo | Risco | Evidência factual | Impacto | Exposição | Mitigação / decisão | Owner / gate | Estado |
|---|---|---|---|---|---|---|---|---|
| R-01 | Claim | Tratar marcas presentes nos nomes do portfólio como clientes/parceiras pode criar alegação não autorizada. | PRD lista marcas no acervo e proíbe essa inferência. [E-PRD §§4, 7.3, 10] | Alto | Alto | Usar “trabalhos registrados no portfólio”; confirmar relação e direitos antes de qualquer claim. | HG-01 | Aberto |
| R-02 | Claim | Converter “desde 1987” em idade numérica pode estar errado sem mês da fundação. | PRD manda não usar “38+ anos”/“39 anos” sem confirmação. [E-PRD §7.7] | Médio | Médio | Usar somente “Desde 1987”. | HG-01 | Aberto |
| R-03 | Operacional | Afirmar instalação, manutenção, prazo ou quantidade mínima sem confirmação. | PRD proíbe preencher essas lacunas por plausibilidade. [E-PRD §§4, 7.8, 7.11] | Alto | Alto | Omitir/usar TBD; obter confirmação operacional antes de FAQ/copy. | HG-01 | Aberto |
| R-04 | Conteúdo | Atribuir material, ano, local ou técnica a um case sem metadata. | PRD manda usar `null` para dado desconhecido. [E-PRD §12] | Médio | Alto | Modelar campos nulos e ocultá-los na UI. | Architecture + HG-01 | Aberto |
| R-05 | Curadoria | Publicar hero/cases sem revisar direitos, qualidade, duplicatas e classificação de “Diversos”. | PRD exige inventário/dedupe/HG-02. [E-PRD §§9–11, 33] | Alto | Alto | Wave 0 antes da seleção; preservar originais; revisão humana. | HG-02 | Aberto |
| R-06 | Validação | Escolher mensagem/CTA por preferência e declarar melhoria sem baseline. | PRD define hipóteses e exige tracking confiável antes de experimentos. [E-PRD §§1.2, 21, 24] | Médio | Alto | Instrumentar, definir métrica e testar uma hipótese por vez. | Analytics / HG-04 | Aberto |
| R-07 | Métrica | Usar benchmark Unbounce como meta específica da Argon-Bras. | PRD diz que não é benchmark para fabricação de comunicação visual brasileira. [E-PRD §23] | Médio | Médio | Criar baseline próprio e separar clique de lead qualificado. | Growth/Analytics | Aberto |
| R-08 | Taxonomia | Publicar “Diversos” ou classificações inferidas como fato. | PRD chama classificação inicial de hipótese analítica visual. [E-PRD §11.3] | Médio | Alto | Curar por asset e registrar confiança; não publicar antes de revisão. | HG-02 | Aberto |
| R-09 | Dados | Reproduzir contato sem validação, inclusive artefatos de texto. | PRD exige validar e-mails/telefones e cita artefato a corrigir. [E-PRD §35] | Alto | Médio | Validar por owner; manter dados de contato fora de copy nova até confirmação. | HG-01 | Aberto |
| R-10 | Escopo | Construir/públicar antes das ondas, gates e aprovação de design/tracking. | PRD ordena Waves e veda publicação sem gate final. [E-PRD §§33, 40] | Alto | Médio | Handoff desta Wave apenas; não publicar. | HG-03/HG-04/HG-05 | Controlado neste trabalho |
| R-11 | Privacidade | Ativar analytics/UTM/CRM sem decisão de ferramentas e consentimento aplicável. | PRD prevê consentimento quando juridicamente necessário e HG-04. [E-PRD §21, §33] | Alto | Médio | Definir ferramentas, dados, retenção e consentimento antes de ativar. | HG-04 | Aberto |
| R-12 | Evidência | Inferir demanda/concorrência/SEO sem fontes permitidas de mercado. | Este trabalho só utilizou PRD e fontes públicas Argon listadas. | Médio | Alto | Marcar mapa de intenção como hipótese; solicitar dados autorizados para validar. | Owner + Research | Aberto |

## Riscos de go/no-go para a próxima onda

### Fato
HG-01 e HG-02 são gates obrigatórios antes de publicação de claims/curadoria; HG-04 cobre tracking/privacy e HG-05 cobre produção. [E-PRD §33]

### Interpretação
A arquitetura/UX pode prosseguir usando campos nulos e texto condicionado, mas copy final, marcas, cases e contatos devem permanecer em estado de aprovação pendente.

### Hipótese
Se os gates forem resolvidos antes do build, reduz-se retrabalho editorial e risco de publicação de alegações incorretas. Isso é uma hipótese operacional, não uma métrica comprovada neste projeto.

## Fontes

- **[E-PRD]** PRD-fonte, §§1, 4, 7, 9–12, 21, 23–24, 33, 35 e 40.
