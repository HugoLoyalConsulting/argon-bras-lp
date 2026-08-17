# Jornada UX — Argon-Bras

**Escopo:** Home/LP principal e padrões reutilizáveis para LPs de serviço.  
**Objetivo dominante:** transformar interesse qualificado em solicitação de orçamento, preservando o portfólio real como prova.  
**Princípio:** ver trabalho antes de aceitar discurso; iniciar orçamento sem burocracia.

## Premissas e limites

- Fatos conhecidos: atuação declarada desde 1987; comunicação visual, letreiros, iluminação, neon, displays/acrílico e trabalhos especiais documentados na PRD.
- Hipóteses: CTA sticky e formulário progressivo podem reduzir atrito; devem ser medidas, não narradas como resultado.
- Dados não confirmados (instalação, prazo, quantidades, materiais por case, relação com marcas) ficam ocultos ou `TBD` até HG-01/HG-02.
- Não há stock como substituto de trabalho Argon-Bras adequado; imagens são curadas e aprovadas antes de aparecerem.

## Persona operacional

| Perfil | Contexto | Pergunta que precisa responder | Necessidade UX |
|---|---|---|---|
| Decisor de marca/varejo | Chega por anúncio ou indicação com demanda de presença física | “Eles fazem o nível e o tipo de letreiro/fachada que preciso?” | proposta clara, prova visual e serviço específico |
| Arquiteto/produção/evento | Tem referência, logo, medida ou foto do local | “Posso explicar um projeto fora do padrão sem perder tempo?” | fluxo de orçamento guiado, upload e descrição |
| Pessoa exploradora | Ainda não conhece a técnica certa | “Qual solução se aplica ao meu caso?” | matriz de serviços com linguagem de aplicação e CTA de orientação |

## Caminho primário: Home → prova → orçamento

| Momento | Intenção do visitante | Interface/resposta | Evidência e evento | Critério de saída |
|---|---|---|---|---|
| 1. Chegada | Entender em segundos | Hero: H1 direto, foto flagship real, “Solicitar orçamento” e “Ver projetos realizados” | `page_view`; hero LCP | visitante consegue dizer o que a Argon-Bras faz |
| 2. Confiança inicial | Avaliar experiência sem leitura longa | Faixa factual “Desde 1987” e projeto personalizado; marcas só como “trabalhos no portfólio” se validadas | `scroll_50` | continua para serviços/cases |
| 3. Encontrar solução | Relacionar necessidade a serviço | Matriz editorial com Letreiros luminosos, Backlight, Letras 3D, Neon, Fachadas/sinalização, Displays/acrílico e Projetos especiais | `view_service`, `cta_click` com `service` e `placement` | abre serviço ou pede orçamento contextual |
| 4. Ver prova | Conferir qualidade e pertinência | Featured Work filtrável; cards mostram apenas metadados confirmados | `view_portfolio_item`, `portfolio_filter` | abre case, continua ou entra no formulário |
| 5. Reduzir incerteza | Saber como começar | Processo de quatro etapas e FAQ factual; perguntas operacionais pendentes ficam fora da resposta pública | `faq_open` | entende o que enviar |
| 6. Converter | Enviar pedido completo | Form de três etapas, progresso textual e CTA único | `form_start`, `form_step_complete`, `form_upload`, `generate_lead` | vê confirmação com lead ID e próximo passo confirmado |

## Caminhos alternativos

### A. Serviço específico → portfolio filtrado → orçamento pré-selecionado

1. Chega em `/letreiros-luminosos`, `/neon` ou outra LP por serviço.
2. O hero faz message match com a intenção e exibe uma imagem relevante aprovada.
3. “Ver projetos” ancora em casos da mesma categoria; filtros preservam a rota/UTM.
4. “Pedir orçamento deste serviço” abre `/orcamento?service=<canônico>` com a opção pré-selecionada e editável.
5. O formulário registra `service`, `landing_page`, `placement`, UTM e origem conforme plano de tracking.

### B. Explorador → “Não sei — quero orientação” → orçamento

1. Na matriz ou no formulário, escolhe “Não sei — quero orientação”.
2. O fluxo não força terminologia técnica; pergunta contexto, local e objetivo na etapa de projeto.
3. Ao submeter, registrar o serviço como `guidance`/valor canônico definido pela arquitetura — nunca inferir automaticamente uma técnica.

### C. Conversão por WhatsApp (quando validado)

1. CTA textual “Falar no WhatsApp” aparece no CTA final e barra inferior pós-hero.
2. O clique registra `whatsapp_click` uma vez com `placement`, página e serviço; não inclui conteúdo livre/PII no evento.
3. Abre deep link apenas com número e mensagem aprovados. Se indisponível, desabilitar a opção e manter formulário como caminho confiável.

## Arquitetura de decisão por seção

```text
Entender oferta
  → Ver prova real
    → Identificar serviço
      → Conferir aplicações/case
        → Entender como funciona
          → Solicitar orçamento
```

A Home não é um catálogo infinito: 6–8 projetos selecionados conduzem à página de portfólio para exploração ampla. O formulário não é uma “página contato” genérica: é o desfecho da jornada.

## Pontos de CTA

| Local | CTA principal | CTA secundário | Regra |
|---|---|---|---|
| Header fixo | Solicitar orçamento | — | visível em todos os breakpoints |
| Hero | Solicitar orçamento | Ver projetos realizados | máximo dois CTAs |
| Service matrix | Ver projetos | Pedir orçamento deste serviço | contextualiza `service` |
| Case/portfolio | Ver detalhes | Solicitar orçamento | não inferir especificações ausentes |
| Final | Solicitar orçamento | Falar no WhatsApp | WhatsApp só após validação |
| Mobile pós-hero | Solicitar orçamento | WhatsApp | barra inferior fixa; oculta dentro do form |

## Acessibilidade e recuperação

- Skip link leva ao `main`; header fixo não bloqueia âncoras (`scroll-margin-top`).
- Todo CTA possui rótulo textual e alvo mínimo 44×44 px; ícone não é a única linguagem.
- Foco acompanha o fluxo, drawer prende foco e fecha com `Esc`.
- Filtros e accordion FAQ operam por teclado e anunciam estado expandido/selecionado.
- Sem hover, a mesma informação dos cards permanece disponível.
- Em erro de formulário, foco vai ao resumo acessível e depois ao primeiro campo inválido; respostas válidas persistem.
- Em falha de rede, não afirmar que o pedido foi enviado; oferecer “Tentar novamente” e canal alternativo somente se confirmado.

## Métricas por hipótese

| Hipótese | Sinal | Decisão posterior |
|---|---|---|
| Prova após hero melhora exploração útil | `view_portfolio_item` e `portfolio_filter` por sessão | comparar depois de baseline confiável |
| Sticky mobile ajuda intenção WhatsApp | `whatsapp_click` por sessão mobile | não confundir clique com lead qualificado |
| Formulário em etapas reduz abandono | `form_start` → `generate_lead`, erros e avanço por etapa | tratar como experimento, não como fato |
| LP por serviço melhora message match | conversão por `landing_page`/`service` | exigir volume e atribuição válidos |

## Critérios de aceite UX

- Em 5 segundos, a primeira dobra responde o que é feito, mostra qualidade real e aponta o orçamento.
- A prova visual ocorre antes de texto institucional longo.
- Nenhuma categoria pública chama-se “Diversos”.
- Todo trajeto chega a orçamento sem depender de menu, hover ou telefone exposto no hero.
- Mobile é pensado de 360–430 px; desktop é ampliação, não redução.
- Estados de menu, portfólio, formulário, erro, sucesso e carregamento estão especificados em `mobile_states.md` e `form_flow.md`.
