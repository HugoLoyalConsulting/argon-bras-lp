# Estados mobile — Argon-Bras

**Viewport de desenho:** 360, 390 e 430 px. **Regra:** mobile é o baseline, não uma versão comprimida do desktop. Testar também safe areas, teclado virtual, zoom 200%, rede lenta e `prefers-reduced-motion`.

## Estrutura persistente

| Elemento | Estado/base | Regras |
|---|---|---|
| Header | fixo, 64 px, `z-index: 50` | logo, CTA compacto e menu; fundo `ink` opaco; reservar espaço no conteúdo |
| CTA inferior | aparece depois da saída do hero | fixa com safe area; altura mínima 56 px; orçamento dominante; não aparece dentro do form/modal |
| Conteúdo | margem lateral 16 px (20 px em 390+) | 4 colunas conceituais/gap 12 px; sem overflow horizontal |
| Foco | anel visível 3 px + offset | existe com teclado, switch access e toque assistivo |
| Motion | sutil e opcional | reduce-motion remove reveal, scale e transições não essenciais |

## 1. Header e menu

### Fechado

```text
[Argon-Bras]                 [Orçamento] [Menu]
--------------------------------------------------
```

- CTA pode usar texto curto “Orçamento” apenas no header mobile; ações no conteúdo usam a redação completa.
- Menu é botão com rótulo acessível “Abrir menu”, área ≥44×44 px e `aria-expanded=false`.
- Header não ganha segunda linha, telefone ou e-mail.

### Aberto

```text
┌──────────────────────────────────────────────┐
│ Argon-Bras                            [Fechar]│
│                                              │
│ Serviços                                    │
│ Portfólio                                   │
│ Sobre                                       │
│                                              │
│ [ Solicitar orçamento ]                     │
└──────────────────────────────────────────────┘
```

- Drawer/modal cobre conteúdo com superfície opaca; sem glass obrigatório.
- Foco entra no título/primeiro link, fica preso no drawer e retorna ao botão menu ao fechar.
- `Esc`, toque no botão fechar e navegação por link encerram o estado. Fundo não rola.
- Links têm 48 px+; CTA tem 52 px.

## 2. Hero

### Estado carregando

- Reservar a proporção da imagem (sem CLS); skeleton neutro, sem shimmer em `reduce-motion`.
- Headline e CTA podem renderizar antes, mas nunca sobre área de contraste indefinido.

### Carregado

```text
[foto real flagship; overlay sólido de leitura]
COMUNICAÇÃO VISUAL • DESDE 1987
Letreiros, luminosos e fachadas que fazem sua marca ser vista.
Projetos personalizados em comunicação visual.
[ Solicitar orçamento ]
[ Ver projetos realizados → ]
```

- H1 em até três linhas a 360 px; imagem é protagonista, mas texto permanece no bloco com contraste AA.
- Sem auto-play, slideshow, vídeo obrigatório ou gesto horizontal oculto.
- O CTA inferior só entra após saída do hero para evitar quatro ações concorrentes na primeira dobra.

### Falha de imagem

- Mantém o H1 e CTAs em fundo `ink`; usar fallback local aprovado se existir.
- Registrar observabilidade técnica; não substituir por stock automaticamente.

## 3. Matriz de serviços e portfolio

### Service matrix

- Sequência vertical assimétrica: primeiro módulo de mídia maior, depois módulos alternados; não replicar uma grade de cards iguais.
- Card é link inteiro com título, imagem, “Ver projetos”; “Pedir orçamento deste serviço” aparece como link auxiliar visível, não somente hover.
- Em loading, preservar cada `aspect-ratio`; em erro, exibir mensagem no bloco e CTA para portfólio/form, sem mentir que há projetos filtrados.

### Filtros de portfolio

```text
Projetos selecionados
[Todos] [Luminosos] [Backlight] [Neon]  → rolagem horizontal apenas dos filtros
[imagem]
Nome do projeto
Categoria confirmada · Aplicação confirmada
Ver detalhes →
```

- Filtros são botões `aria-pressed`, com texto; faixa pode rolar horizontalmente e oferece foco claro, sem esconder conteúdo principal.
- Resultado de filtro anuncia “N projetos exibidos” em `aria-live=polite`.
- Estado vazio: “Ainda não há projetos publicados nesta seleção.” Oferecer “Ver todos os projetos” e “Solicitar orientação”; não usar “Diversos”.
- Estado erro: “Não foi possível carregar os projetos. Tente novamente.” com retry.
- Metadados `null` são omitidos, não preenchidos com suposições.

### Case/detail

- Imagem ocupa largura integral ou sangra para borda com crop aprovado; informações em coluna legível abaixo.
- Botão voltar preserva filtro quando possível; CTA contextual conserva `service`.
- Modal de imagem, se existir, tem fechar, foco preso, descrição e alternativa de navegação por teclado; não é requisito para compreender o case.

## 4. FAQ

- Acordeon de uma coluna; botão de 48 px+, ícone complementar a “expandir/recolher”, `aria-expanded` e `aria-controls`.
- Pode haver vários itens abertos; não depende de animação de altura.
- FAQ com resposta operacional não confirmada fica oculto até HG-01; não preencher com resposta genérica.

## 5. Formulário de orçamento

### Base (cada etapa)

```text
← Voltar                 Etapa 2 de 3
Como podemos falar com você?
Usaremos estes dados para responder ao seu pedido.

Nome *
[________________________________]

WhatsApp *
[________________________________]

[ Continuar ]
```

- Um `h1`/título de fluxo e progresso textual; indicador visual não é a única informação.
- Ao abrir teclado, página rola o campo para área segura; CTA inferior fixa é ocultada.
- Ação primária em largura total no mobile; secundária é link/botão menos proeminente.

### Erro de validação

```text
Há campos a revisar.
WhatsApp *
[ valor                         ]
Informe um WhatsApp com DDD.
```

- Resumo recebe foco após tentativa; campo possui erro textual, `aria-invalid` e não perde conteúdo.
- Cor vermelha é suplemento; ícone e mensagem deixam significado explícito.

### Upload

- Antes de selecionar: botão “Adicionar logo (opcional)”; limite/formato apenas se realmente configurado.
- Durante: nome legível, progresso e “Cancelar”.
- Falha: arquivo e motivo seguro; “Tentar novamente”.
- Se upload não estiver implementado de ponta a ponta, controle não aparece.

### Enviando, sucesso e falha

| Estado | Conteúdo | Próxima ação |
|---|---|---|
| enviando | “Enviando pedido…” no botão; inputs bloqueados | aguardar sem spinner isolado |
| sucesso | “Recebemos seu pedido.” + lead ID, se retornado | voltar ao portfólio ou WhatsApp validado |
| rede/servidor | “Não foi possível enviar agora. Seus dados continuam nesta página.” | Tentar novamente |
| sessão expirada | explicar que o envio não foi confirmado | revisar e reenviar; não declarar sucesso |

## 6. Barras, drawers, modais e estados de sistema

| Superfície | Comportamento mobile |
|---|---|
| Bottom CTA | fixa após hero; `bottom: max(12px, env(safe-area-inset-bottom))`; sombra moderada; não sobrepõe formulário |
| Cookie/consentimento, se necessário | não compete com bottom CTA; pode empilhar acima e respeita safe area; decisão HG-04 |
| Modal | somente para tarefa que não cabe na página; fundo opaco, scroll interno, fechar evidente, foco preso |
| Toast | não é única confirmação de submit; `aria-live`, tempo suficiente, não cobre CTA/campo |
| Offline | banner textual discreto; formulário não alega envio enquanto offline |

## Matriz de validação responsiva

| Largura | Verificar |
|---:|---|
| 360 | H1 em 2–3 linhas, header não colide, CTA inferior não cobre conteúdo, sem overflow |
| 390 | base de aprovação visual mobile; campos e fotos com crop intencional |
| 430 | CTA/header continuam compactos, não criam falsas duas colunas |
| 768 | menu e matriz transicionam sem salto; grid 8 colunas |
| 1024 | header 72 px, CTA desktop visível, conteúdo 12 colunas inicia |
| 1280/1440 | composição editorial ganha espaço, container limita em 1440 |
| 1920 | whitespace cresce; texto, imagens e linhas de leitura não ficam excessivos |

## Checklist de aceite mobile

- [ ] Header é fixo de fato e âncoras não ficam escondidas.
- [ ] Menu, CTA, filtros, accordion e form funcionam por teclado e toque.
- [ ] Targets possuem mínimo 44 px; form/CTA preferem 52 px.
- [ ] Há estado loading/empty/error/success explícito para mídia e formulário.
- [ ] Imagens têm proporção reservada, crop mobile aprovado e texto com AA.
- [ ] Bottom CTA respeita safe area, não duplica ação no form e não encobre teclado.
- [ ] Nenhuma informação depende exclusivamente de hover, cor, animação ou ícone.
- [ ] `prefers-reduced-motion` elimina motion decorativo.
