# SOP_DELTA — UX Architect + UI/Brand | Argon-Bras

```yaml
sop_id: "SOP-LP-005, SOP-LP-009, SOP-LP-010, SOP-LP-011, SOP-LP-012, SOP-LP-016"
sop_version_used: "PRD Argon-Bras v1.0 / 2026-08-16"
agent: "UX Architect + UI/Brand"
task_id: "ARGONBRAS-UXUI-001"
date: "2026-08-16"
what_worked:
  - "Traduzir a mistura 75% editorial / 25% componentizada em regras verificáveis, em vez de imitar referências visuais."
  - "Tratar fotografia real como componente de prova: cada imagem possui função, crop e fallback; dados sem confirmação são ocultos."
  - "Especificar navegação fixa e CTA inferior mobile com regras de safe area, foco e exclusão durante o formulário."
what_failed:
  - "A PRD fornece direção de paleta, mas não uma extração validada do logo nem assets curados; a cor de ação é uma proposta, não um atributo de marca aprovado."
  - "Não há confirmação operacional para promessa de prazo, instalação, manutenção, WhatsApp deep link, backend de uploads ou copy final de privacidade."
new_pattern:
  name: "Editorial Proof + System States"
  rule: >-
    Para LPs portfolio-led, desenhar primeiro a sequência afirmação → imagem real →
    detalhe confirmado → CTA; em paralelo, especificar os mesmos componentes em
    default, foco, loading, vazio, erro e sucesso. A composição pode variar; o
    comportamento nunca fica implícito.
anti_pattern:
  - "Converter uma direção premium em grade 3×N de cards iguais, labels excessivos ou superfícies de glassmorphism."
  - "Usar texto diretamente sobre fotografia sem medir contraste no crop e overlay finais."
  - "Desenhar upload, WhatsApp ou sucesso de formulário como funcional antes de validar o caminho técnico end-to-end."
new_check:
  - "Antes do handoff para build, validar 390 px e 1440 px para header fixo, hero, matriz, projeto, formulário e CTA inferior."
  - "Para cada conteúdo de portfolio, exigir evidência de categoria/aplicação; campos nulos são ocultados em vez de inferidos."
  - "Medir contraste final em toda combinação de texto/superfície e em cada overlay de imagem; AA para texto normal, foco >=3:1."
  - "Verificar que a barra mobile fixa não disputa a primeira dobra e some no fluxo de orçamento/teclado."
tool_notes:
  - "O lint automático do repositório não processa Markdown; DESIGN.md requer lint dedicado via @google/design.md quando o ambiente permitir."
  - "Usar inspeção visual de assets oficiais antes de consolidar cor de acento, crop e hero."
decision_rule: >-
  Quando houver conflito entre um efeito visual e legibilidade, performance,
  evidência factual ou fluxo de orçamento, escolher a segunda opção. Quando um
  dado não tiver fonte confirmada, marcar TBD/ocultar e encaminhar ao Human Gate,
  nunca completar por plausibilidade.
evidence:
  - "PRD Argon-Bras v1.0: seções 5, 7, 13–18, 28.4–28.5, 33–35 e 43–47."
  - "design/DESIGN.md"
  - "ux/journey.md"
  - "ux/form_flow.md"
  - "ux/mobile_states.md"
recommended_change: >-
  Incorporar no SOP-LP-009 uma checagem explícita de nav position: fixed,
  scroll-offset, safe area e supressão da bottom CTA durante o form. Incorporar
  no SOP-LP-010/011 a proibição de aprovar paleta/hero sem amostras reais e uma
  matriz de Taste QA que teste variedade de escala, prova visual e ausência de
  cardificação. Incorporar no SOP-LP-012 a regra de não expor upload/WhatsApp
  como caminho operacional sem validação técnico-legal.
confidence: "high"
review_required: true
```

## Delta acionável para revisão da Fábrica

1. **SOP-LP-009 — Mobile-First LP Review:** acrescentar validação por viewport 360/390/430, safe areas, teclado virtual, header fixo, `scroll-margin-top`, modal/drawer com foco preso e CTA inferior que não encobre formulário.
2. **SOP-LP-010 — DESIGN.md Generation:** exigir que os tokens declarem cor, tipografia, espaço, raios, contraste e componentes, mas marquem como *proposta* qualquer cor derivada sem inspeção de logo/ativos. Exigir ratio de contraste escrito e regras para texto sobre imagem.
3. **SOP-LP-011 — Taste/FlutterFlow UI QA:** separar composição editorial de padronização comportamental. Aprovar variedade controlada de escala/ritmo, porém cobrar estados completos e componentes acessíveis. Falhar em UI genérica, excesso de cards, pills, gradiente padrão, glass indiscriminado e motion decorativo.
4. **SOP-LP-012 — Form Funnel Design:** condicionar upload, mensagem de WhatsApp, consentimento, prazo e confirmação a capacidade/decisão comprovada. `generate_lead` só após sucesso confirmado e com prevenção de duplicidade.

## Handoff

| Consumidor | Artefato | Ação necessária |
|---|---|---|
| Creative / Portfolio curation | `design/DESIGN.md` | submeter logo, hero, crops e 6–8 featured cases ao HG-02/HG-03 |
| Full-Stack Builder | `design/DESIGN.md`, `ux/*.md` | implementar tokens, navegação fixa real, estados e semântica sem reinterpretar UX |
| QA / A11y | `ux/mobile_states.md`, `ux/form_flow.md` | testar matriz responsiva, foco, reduced motion, contrastes finais, erros e submit end-to-end |
| Product / Legal / Analytics | `ux/form_flow.md` | decidir dados, privacidade, uploads, eventos e canais antes de ativação |

**Status:** delta substancial para revisão humana; não altera SOPs globais nem autoriza publicação.
