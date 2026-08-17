# Mapa de intenção de busca — Argon-Bras

**Status:** hipótese de arquitetura e mensagem; não é pesquisa de palavra-chave.
**Regra de evidência:** não há dados de Search Console, tendências, SERP, volume, CPC ou concorrência nas fontes permitidas. Nenhuma linha abaixo afirma demanda, ranking ou desempenho orgânico.

## Base factual

- O PRD define o Job-to-be-Done como avaliar se a Argon-Bras consegue executar comunicação visual para fachada, letreiro, logo tridimensional, iluminação, neon ou peça especial, ver projetos semelhantes e iniciar orçamento. [E-PRD §2.2]
- O site público lista letreiros, neons, luminosos, fachadas e displays; Serviços descreve letras-caixa, neon, bandeja/display e luminárias em acrílico. [E-SITE-HOME; E-SITE-SERVIÇOS]
- O PRD recomenda rotas de serviço e exige message match entre anúncio e LP específica. [E-PRD §5.2, §6]

## Mapa operacional

| Cluster de intenção **hipotético** | Necessidade expressa pelo visitante | Página/conteúdo recomendado | Prova permitida | CTA dominante | Status de validação |
|---|---|---|---|---|---|
| Letreiro luminoso | Entender opções de letreiro iluminado e iniciar orçamento | `/letreiros-luminosos` | Imagens de iluminação frontal do acervo após curadoria | Solicitar orçamento | Oferta factual; intenção de busca não mensurada |
| Backlight/iluminação indireta | Ver efeito de iluminação traseira e trabalhos semelhantes | `/backlight` | Grupo público “iluminação traseira / backlight” após HG-02 | Pedir orçamento deste serviço | Oferta factual; intenção não mensurada |
| Letras-caixa / logo 3D | Avaliar letras e logotipos sem iluminação ou materiais | `/letras-caixa` | Serviço e materiais apenas como declarados em Serviços | Solicitar orçamento | Oferta factual; copy técnica depende de confirmação por projeto |
| Neon personalizado | Ver exemplos de neon e informar o projeto | `/neon` | Grupo Neon do portfólio após curadoria | Falar sobre meu projeto / Solicitar orçamento | Oferta factual; termo e CTA a testar |
| Fachada/sinalização | Avaliar comunicação visual aplicada a fachada | `/fachadas-sinalizacao` | Somente assets revisados para essa aplicação | Solicitar orçamento | Oferta declarada; aplicação de assets pendente |
| Display/acrílico | Entender bandejas, displays, PETG e luminárias em acrílico | `/displays-acrilico` | Texto de Serviços e assets aprovados | Pedir orçamento deste serviço | Oferta factual; uso/volume não mensurados |
| Projeto fora da taxonomia | Enviar necessidade ainda não classificada | `/projetos-especiais` e orçamento | Apenas portfólio revisado | Quero orientação | Hipótese de desambiguação |
| Avaliação de fornecedor | Ver trabalho, histórico e como começar | Home/portfólio/cases | “Desde 1987”, acervo real e contato público | Ver projetos → Solicitar orçamento | Fluxo recomendado no PRD; impacto não medido |

## Regras de message match

### Fatos
- O PRD dá os exemplos `letreiro luminoso → /letreiros-luminosos`, `neon → /neon` e stands → `/projetos-especiais/stands-eventos`. [E-PRD §5.2]
- O PRD define “Solicitar orçamento” como objetivo dominante de LP de tráfego pago. [E-PRD §5.1]

### Interpretação
- Uma página genérica não é a melhor superfície de mensagem quando a origem já carrega um serviço específico.
- A página específica deve apresentar primeiro a solução e o portfólio relacionado; terminologia técnica sem contexto visual pode aumentar ambiguidade.

### Hipóteses de teste futuro
1. **H-INT-01:** uma LP específica por serviço terá melhor match percebido que a Home genérica para tráfego com intenção específica.
2. **H-INT-02:** “Solicitar orçamento” e “Falar sobre meu projeto” podem produzir comportamentos distintos; escolher somente após instrumentação e baseline.
3. **H-INT-03:** um formulário em três etapas pode reduzir atrito percebido em comparação a uma única tela longa.

Nenhuma hipótese deve ser experimentada antes de tracking confiável, métrica definida e volume razoável, conforme PRD. [E-PRD §24]

## Dados necessários para transformar o mapa em pesquisa validada

| Dado ausente | Uso | Gate/owner sugerido |
|---|---|---|
| Consultas, impressões, CTR e páginas de destino (Search Console) | Priorizar linguagem, rotas e conteúdo | Owner + Growth/Analytics; HG-04 quando envolver tracking |
| Source/medium/campaign e UTMs | Avaliar message match por origem | Product Architect/Analytics |
| Eventos `view_service`, `cta_click`, `whatsapp_click`, `form_start`, `generate_lead` | Medir progressão no funil | Product Architect/Analytics |
| Serviço solicitado e qualidade do lead | Separar clique de solicitação qualificada | Comercial/CRM + Analytics |
| Perguntas reais de orçamento | Refinar FAQ, formulário e microcopy | Comercial; HG-01 para novas alegações |

## Fontes

- **[E-SITE-HOME]** https://www.luminososargonbras.com/
- **[E-SITE-SERVIÇOS]** https://www.luminososargonbras.com/servicos
- **[E-PRD]** PRD-fonte, §§2.2, 5.1–5.2, 6, 12, 21 e 24.
