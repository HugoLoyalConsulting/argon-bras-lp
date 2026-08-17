---
version: alpha
name: Argon-Bras Editorial Portfolio System
description: Sistema mobile-first, editorial e neutro para uma vitrine de comunicação visual construída sobre fotografia real de trabalhos Argon-Bras.
colors:
  primary: "#A94A27"
  ink: "#111314"
  ink-raised: "#1B1E20"
  ink-subtle: "#25292B"
  canvas: "#F5F2EC"
  canvas-raised: "#FFFCF7"
  text-on-dark: "#F8F6F1"
  text-on-light: "#17191A"
  text-muted-dark: "#C9CBC8"
  text-muted-light: "#565B5C"
  line-dark: "#454A4A"
  line-light: "#D3D0C9"
  accent: "#A94A27"
  accent-hover: "#853618"
  success: "#176B4D"
  error: "#A42424"
typography:
  display:
    fontFamily: "Manrope, Inter, Arial, sans-serif"
    fontSize: "6.5rem"
    fontWeight: 650
    lineHeight: 0.98
    letterSpacing: "-0.055em"
  h1:
    fontFamily: "Manrope, Inter, Arial, sans-serif"
    fontSize: "5.5rem"
    fontWeight: 650
    lineHeight: 1.0
    letterSpacing: "-0.05em"
  h2:
    fontFamily: "Manrope, Inter, Arial, sans-serif"
    fontSize: "4rem"
    fontWeight: 650
    lineHeight: 1.05
    letterSpacing: "-0.04em"
  h3:
    fontFamily: "Manrope, Inter, Arial, sans-serif"
    fontSize: "1.75rem"
    fontWeight: 650
    lineHeight: 1.15
    letterSpacing: "-0.025em"
  body:
    fontFamily: "Manrope, Inter, Arial, sans-serif"
    fontSize: "1rem"
    fontWeight: 450
    lineHeight: 1.55
    letterSpacing: "0em"
  label:
    fontFamily: "Manrope, Inter, Arial, sans-serif"
    fontSize: "0.75rem"
    fontWeight: 700
    lineHeight: 1.25
    letterSpacing: "0.1em"
rounded:
  control: 12px
  media: 18px
  large-media: 24px
  pill: 999px
spacing:
  1: 4px
  2: 8px
  3: 12px
  4: 16px
  5: 24px
  6: 32px
  7: 48px
  8: 64px
  9: 96px
  10: 128px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.text-on-dark}"
    typography: "{typography.body}"
    rounded: "{rounded.control}"
    padding: 16px
    height: 52px
  button-primary-hover:
    backgroundColor: "{colors.accent-hover}"
    textColor: "{colors.text-on-dark}"
    rounded: "{rounded.control}"
    padding: 16px
    height: 52px
  button-secondary-dark:
    backgroundColor: "transparent"
    textColor: "{colors.text-on-dark}"
    typography: "{typography.body}"
    rounded: "{rounded.control}"
    padding: 16px
    height: 52px
  input-light:
    backgroundColor: "{colors.canvas-raised}"
    textColor: "{colors.text-on-light}"
    typography: "{typography.body}"
    rounded: "{rounded.control}"
    padding: 16px
    height: 52px
---

## Overview

**Argon-Bras é uma vitrine de trabalho físico, não uma interface de software.** O sistema enquadra fotografias reais de fachadas, letras, neon e peças especiais com uma linguagem sóbria, arquitetônica e segura. A proporção é **75% editorial** — escala, silêncio visual, crops e sequenciamento — e **25% sistema de componentes** — comportamento previsível, estados explícitos e responsividade disciplinada.

A referência é de postura, não de layout, marca, assinatura ou composição copiável. Não reproduzir grids, marcas, templates ou microinterações de qualquer referência. A especificidade vem do acervo Argon-Bras e de dados confirmados.

**Princípios inegociáveis**

1. Fotografia real é a prova e tem precedência sobre decoração.
2. Um viewport tem uma intenção dominante: entender, explorar ou solicitar orçamento.
3. A interface permanece neutra para não competir com cores, luzes e materiais dos projetos.
4. Clareza comercial vence metáforas publicitárias; não há promessas, números, materiais ou serviços sem evidência.
5. Mobile é a tela-base; desktop amplia composição e nunca esconde caminho de conversão.

## Colors

A paleta é deliberadamente curta. Grafite protege o drama das imagens; off-white aquece os momentos de explicação e formulário; terracota é sinal de ação, não uma cor decorativa ou “neon”. A cor de marca definitiva deve passar por HG-03 após inspeção do logo oficial e amostras do acervo.

| Papel | Token | Uso |
|---|---|---|
| fundo editorial | `ink` | hero, portfólio, case e footer |
| fundo elevado escuro | `ink-raised` | header fixo após scroll, drawers e controles escuros |
| fundo claro | `canvas` | processo, FAQ e orçamento |
| superfície clara | `canvas-raised` | campos e mensagens; opaca, não glass |
| ação principal | `accent` | um CTA primário por contexto e foco selecionado |
| sucesso/erro | `success` / `error` | estado textual + ícone; jamais como único sinal |

Contraste normativo (sRGB): `text-on-dark` em `ink` ≈ 17:1; `text-on-light` em `canvas` ≈ 16:1; `text-muted-dark` em `ink` ≈ 12:1; `text-muted-light` em `canvas` ≈ 6.4:1; `text-on-dark` em `accent` ≈ 5.0:1. Assim, texto normal atende AA (>=4.5:1). Não colocar texto diretamente sobre fotografia sem camada sólida/gradiente que preserve o contraste aferido no crop final.

## Typography

Usar **Manrope** como única família inicial, com subset Latin e pesos 450, 550, 650 e 700 no máximo. É uma família sem serifa com precisão técnica e boa leitura em PT-BR. `font-display: swap`; fallback `Inter, Arial, sans-serif`. Uma família display adicional só pode ser proposta no HG-03 com teste de carga, acentos e ruptura real de linha.

- Display/H1: títulos curtos, sem caixa alta integral; máximo de 2–3 linhas em 360 px para o H1 do hero.
- H2: abrir seções e cases; não competir com a imagem do bloco.
- Label: caixa alta somente para eyebrow, etapa, categoria ou metadado confirmado; evitar excesso de labels.
- Corpo: mínimo 16 px; textos auxiliares mínimo 14 px e contraste AA.
- Números e medidas usam tabular figures quando disponíveis (`font-variant-numeric: tabular-nums`).

## Layout

### Mobile-first

| Faixa | Largura | Comportamento |
|---|---:|---|
| base | 360–479 px | 4 colunas conceituais, margem 16 px (20 px em 390+), gap 12 px |
| compacto | 480–767 px | 4/6 colunas fluídas, imagens ainda prioritariamente empilhadas |
| tablet | 768–1023 px | 8 colunas, margem 32 px, matriz de serviços em 2 áreas |
| desktop | 1024–1439 px | 12 colunas, margem 40–64 px, máximo 1440 px |
| amplo | 1440+ px | container máximo 1440 px; whitespace cresce, conteúdo não estica |

Use Flex/Grid/Wrap e valores fluídos; não dependa de posicionamento absoluto para conteúdo. Toda imagem declara proporção (`aspect-ratio`) e dimensões para prevenir CLS. A solução matrix nasce como sequência vertical de cartões de mídia assimétricos no mobile e se rearranja apenas a partir de tablet.

Ritmo: 64 px entre seções no mobile, 96–128 px no desktop; 24–32 px entre título e conteúdo. O whitespace é estrutural, não uma lacuna para preencher com badges.

### Navegação realmente fixa

O header é `position: fixed; inset: 0 0 auto 0; z-index: 50`, tem **64 px** no mobile e **72 px** no desktop, e reserva no documento `padding-top` correspondente. Fundo inicialmente `ink` opaco; após o início do scroll pode usar `ink-raised` a 96% com borda `line-dark`, sem depender de blur. O logo leva à home; desktop mostra Serviços, Portfólio e Sobre; CTA “Solicitar orçamento” permanece visível. Mobile mostra logo, CTA compacto e botão menu de 44×44 px.

O menu mobile abre em drawer/modal com foco preso, `Esc` para fechar, links de no mínimo 48 px e retorno de foco ao acionador. Ao navegar por âncoras, aplicar `scroll-margin-top: 88px`. Não criar segunda barra fixa.

Após o hero, exibir barra inferior fixa mobile (`bottom: max(12px, env(safe-area-inset-bottom))`) com **Solicitar orçamento** como ação dominante e WhatsApp como ação secundária quando o número e deep link estiverem confirmados. A barra mede 56 px de alvo, não encobre campos focados e se oculta no formulário para evitar duplicação de CTA.

### Estrutura da home

1. Header fixo.
2. Hero de uma fotografia flagship real + overlay de contraste sólido; eyebrow “Comunicação visual • desde 1987”, H1, dois CTAs.
3. Faixa factual de autoridade (desde 1987, personalizado, sob medida, atuação conforme fonte). Não listar marcas como clientes sem validação.
4. Solution Matrix editorial: 7 famílias comerciais, não quatro cards idênticos e nunca “Diversos”.
5. Projetos selecionados: 6–8 imagens reais com categoria/aplicação confirmadas ou ocultas.
6. Case spotlight com campos nulos ocultados.
7. Institucional curto, processo, diferenciais verificáveis, aplicações validadas e FAQ com respostas operacionais confirmadas.
8. Fluxo de orçamento e CTA final.
9. Footer essencial.

## Elevation & Depth

Superfícies são majoritariamente planas, opacas e separadas por mudança de tom, espaço ou borda de 1 px. Sombras só em header fixo, bottom CTA, drawer, modal e popover: `0 12px 32px rgba(0,0,0,.24)`. Não usar glassmorphism como textura de página, cartão ou formulário. Se uma fotografia exigir overlay, usar camada de leitura sólida/gradiente por trás do texto; blur é opcional e nunca a única medida de contraste.

## Shapes

Raio moderado: controles 12 px, mídia 18 px e imagens editoriais grandes 24 px. Evitar pills salvo filtros, tags de estado e controles inerentemente compactos. Não arredondar toda seção ou todo container. Bordas são sutis (`line-dark`/`line-light`) e não substituem hierarquia.

## Components

### Ações e links

- **Primário:** terracota, texto claro, 52 px de altura; um por bloco de decisão. `hover` escurece; `active` reduz 1 px; `focus-visible` é anel de 3 px claro/escuro com offset de 3 px e contraste >=3:1.
- **Secundário:** link sublinhado ou botão contornado, nunca rivaliza com o primário. Setas movem no máximo 4 px em 180 ms.
- **WhatsApp:** rótulo textual “Falar no WhatsApp”; não usar apenas ícone. Usar somente deep link e telefone confirmados; registrar intenção como evento sem PII.

### Mídia e portfólio

`ProjectCard` contém imagem, nome de marca/projeto, categoria e aplicação somente quando confirmados, mais “Ver detalhes”. Em hover pode revelar metadados; no toque eles já ficam visíveis. `FeaturedProject` varia proporção e escala por posição editorial. Não há carrossel automático. Alt descreve o que é visível, sem presumir relação comercial.

### Formulário

Campos claros e opacos em fundo claro; label persistente acima do campo; placeholder é exemplo, não label. Altura mínima 52 px; file upload também recebe botão de 44 px+. Validação é inline, textual e associada por `aria-describedby`; erro usa ícone + texto, não apenas vermelho. O botão mantém estado loading e impede double submit. Campos opcionais são explicitamente marcados.

### Estados obrigatórios

Todo componente interativo especifica default, hover (quando aplicável), focus-visible, active, disabled e loading. Formulário também exige untouched, valid, invalid, upload-progress, submit-error e success. Portfolio exige loading/skeleton com proporção fixa, vazio, erro/retry e resultado filtrado sem conteúdo essencial escondido em hover.

## Do's and Don'ts

**Fazer**
- Selecionar hero e crops a partir de imagens reais aprovadas no HG-02.
- Usar assimetria com alinhamento e informação escaneável.
- Deixar uma ação evidente em cada ponto de decisão.
- Garantir HTML semântico, ordem de foco lógica, skip link e foco sempre visível.
- Respeitar `prefers-reduced-motion`; transições de 150–350 ms, apenas opacity/transform quando possível.

**Não fazer**
- Não copiar referências, layouts, paletas proprietárias ou assinaturas de Taste/FlutterFlow.
- Não usar roxo-gradiente, blobs, UI cyberpunk, contadores, logos de clientes, depoimentos ou métricas inventadas.
- Não usar slideshow hero, vídeo obrigatório, parallax pesado, scroll hijacking ou animação em tudo.
- Não transformar todas as seções em cards nem aplicar glassmorphism indiscriminado.
- Não colocar texto pequeno ou CTA sem proteção de contraste sobre foto.
- Não publicar, substituir imagens, confirmar claims ou efetivar tracking sem os Human Gates aplicáveis.

## Human Gate — HG-03 Design Direction

**Status deste documento: proposta pronta para revisão; não é aprovação de build ou publicação.**

Aprovação humana obrigatória antes de multiplicar telas ou implementar integralmente:

1. Logo oficial, uso de marca e tom do acento terracota contra amostras reais do acervo.
2. Fotografia hero, crops mobile/desktop, seleção de 6–8 projetos e qualquer marca nominada (em conjunto com HG-02/HG-01).
3. Uma tela mobile (390 px) e uma desktop (1440 px) contendo hero, matriz, portfolio, formulário e navegação fixa real.
4. Contraste aferido no crop final, tipografia carregada, foco, drawer e bottom CTA em dispositivo real.
5. Taste QA: foco por viewport, imagens protagonistas, variedade de escala, nenhuma grade 3×N repetitiva ou efeito ornamental sem função.

Aprovar, pedir ajustes ou bloquear deve ser registrado no `00-admin/decision_log.md`; pendências factuais permanecem `TBD`/ocultas. HG-03 não substitui HG-01 (claims), HG-02 (curadoria), HG-04 (tracking/privacidade) ou HG-05 (release).
