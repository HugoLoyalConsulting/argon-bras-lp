# Hipóteses de mensagem — Argon-Bras

**Status:** backlog de validação; não executar teste nem publicar automaticamente.
**Princípio:** hipótese não é claim factual, resultado nem recomendação definitiva.

## Invariantes factuais para todas as variantes

- A oferta pode mencionar comunicação visual, letreiros, neons, luminosos, fachadas e displays, pois o site atual os declara. [E-SITE-HOME]
- Pode usar “Desde 1987” de modo literal. [E-SITE-HOME]
- Pode mostrar trabalhos do portfólio após curadoria, mas não chamar marcas de clientes/parceiras sem HG-01. [E-PRD §7.3, §33]
- Não incluir métricas, prazos, instalação, manutenção, preço, quantidade mínima ou resultados não confirmados. [E-PRD §4]

## Hipóteses priorizadas

| ID | Variante/candidata | Racional *(interpretação)* | Resultado esperado *(hipótese)* | Métrica de decisão | Proteções e pré-requisitos |
|---|---|---|---|---|---|
| MSG-01 | **“Letreiros, luminosos e fachadas que fazem sua marca ser vista.”** | Nomeia oferta e resultado visual de forma direta. | Pode melhorar entendimento em cinco segundos versus H1 institucional. | entendimento qualitativo; `cta_click`; `form_start` | Comparar uma variável; tracking validado; não prometer impacto comercial. |
| MSG-02 | **“Projetos personalizados em comunicação visual, de letras-caixa e backlight a neon, fachadas, displays e peças especiais.”** | Explica amplitude sem superlativo. | Pode reduzir dúvida sobre escopo para visitantes com projeto definido. | `view_service`; CTA por serviço; campo “o que procura” | Serviços/termos devem continuar confirmados por HG-01. |
| MSG-03 | **“Desde 1987, construindo marcas para serem vistas.”** | Usa histórico declarado como apoio de confiança. | Pode aumentar confiança percebida quando acompanhado de prova visual. | pesquisa qualitativa; avanço para portfólio/orçamento | Não converter em idade numérica; não usar como prova de liderança. |
| MSG-04 | **“Veja trabalhos registrados no nosso portfólio.”** | Evita inferir vínculo comercial de marcas. | Pode conduzir para prova sem risco de claim de cliente. | `view_portfolio_item`; `cta_click` subsequente | Hero/cases e direitos aprovados em HG-02. |
| MSG-05 | CTA A: **“Solicitar orçamento”**; CTA B: **“Falar sobre meu projeto”** | A é objetiva; B pode reduzir pressão percebida. | Uma variante pode gerar mais solicitações qualificadas, não apenas cliques. | `generate_lead` e qualidade de lead, não CTR isolado | Experimento posterior a baseline; uma hipótese por teste. |
| MSG-06 | CTA de portfolio: **“Ver projetos realizados”** | Enquadra a galeria como evidência antes da conversão. | Pode apoiar avaliação antes de iniciar orçamento. | `view_portfolio_item` → `form_start`/`whatsapp_click` | Não interpretar correlação como causalidade sem desenho de teste. |

## Ordem de mensagem recomendada para prototipação

### Fato
O PRD define a sequência “afirmação → imagem real → detalhe técnico → CTA” e indica proposta clara, prova visual e orçamento como estrutura de Home. [E-PRD §§5.3, 7]

### Interpretação
Uma primeira dobra pode combinar:
1. oferta direta (MSG-01);
2. explicação curta de amplitude (MSG-02);
3. imagem real curada;
4. CTA de orçamento (MSG-05 A) e CTA de portfólio (MSG-06).

### Hipótese
Essa ordem pode fazer o visitante entender o que a empresa faz, ver prova e saber como começar com menos leitura institucional. A hipótese só pode ser considerada apoiada após mensuração/avaliação qualitativa.

## Plano mínimo de validação futura

1. **Antes do teste:** instrumentar eventos e parâmetros do PRD, validar disparo único e definir lead qualificado. [E-PRD §21]
2. **Baseline:** registrar comportamento da versão aprovada sem declarar meta externa; o benchmark Unbounce é explicitamente direcional e não específico da Argon-Bras. [E-PRD §23]
3. **Teste:** alterar somente uma hipótese por vez, por exemplo CTA A/B ou imagem flagship/mosaico. [E-PRD §24]
4. **Leitura:** separar clique de WhatsApp, início de formulário, envio e solicitação qualificada. [E-PRD §§2.3–2.4, 23]
5. **Gate:** qualquer novo claim factual vai a HG-01; qualquer novo uso de marca/asset vai a HG-02.

## Fontes

- **[E-SITE-HOME]** https://www.luminososargonbras.com/
- **[E-PRD]** PRD-fonte, §§2, 4, 5, 7, 21, 23–24 e 33.
