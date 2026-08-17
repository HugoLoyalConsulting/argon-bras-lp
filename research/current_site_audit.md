# Auditoria do site atual — Argon-Bras

**Data da evidência pública:** 2026-08-16.
**Escopo:** Home, Serviços, Portfólio, Sobre e Contato listados no PRD.
**Método:** leitura do PRD e consulta HTTP pública das cinco URLs; não houve login, alteração, envio de formulário ou publicação.

## Inventário de superfícies

| URL | Estado técnico observado | Conteúdo factual registrado | Papel atual inferido |
|---|---|---|---|
| `/` | HTTP 200; título HTML observado: “Comunicação Visual \| Argon Bras \| São Paulo”; 36 elementos `img` encontrados no HTML. [E-LIVE-01] | H1 “Argon-Bras Luminosos”; texto de comunicação visual, serviços e “Desde 1987”. [E-LIVE-01; E-PRD §1.1] | Institucional com galeria e contato. |
| `/servicos` | HTTP 200. [E-LIVE-02] | Quatro grupos: letras/logotipos bloco/caixa, neon, bandeja/display e luminárias em acrílico. [E-PRD §1.1] | Descrição de oferta por técnica/categoria. |
| `/portfolio` | HTTP 200. [E-LIVE-03] | 38 imagens nomeadas em cinco grupos, segundo inventário do PRD. [E-PRD §10] | Galeria de trabalhos. |
| `/sobre` | HTTP 200. [E-LIVE-04] | Página indicada como institucional no menu público. [E-PRD §1.1, §52] | Conteúdo institucional. |
| `/contato` | HTTP 200. [E-LIVE-05] | Telefone/WhatsApp, dois e-mails, Instagram, endereço e formulário de orçamento; há galeria adicional sem nomes semânticos no HTML rastreado pelo PRD. [E-PRD §1.1] | Contato/orçamento. |

## Fatos observados

1. A Home comunica empresa de comunicação visual, expertise em letreiros, neons, luminosos, fachadas e displays, e declara operação desde 1987. [E-LIVE-01; E-PRD §52]
2. Serviços declara letras-caixa com iluminação frontal, traseira ou sem iluminação e lista chapa galvanizada pintada, inox, PVC expandido, acrílico e latão. [E-PRD §1.1, §52]
3. Serviços menciona PETG e possibilidade de produção em massa para bandeja/display, além de acrílico transparente gravado e cortado a laser para luminárias. [E-PRD §1.1]
4. O Portfólio é inventariado pelo PRD com 38 imagens nomeadas: 9 frontal, 6 backlight, 11 tipo bloco, 6 neon e 6 diversos. [E-PRD §10]
5. Contato disponibiliza canais públicos e formulário de orçamento. [E-PRD §1.1, §52]
6. O HTML público da Home contém link para WhatsApp e `tel:`; o número observado é `(11) 4582-1572`. [E-LIVE-01]

## Interpretações de UX/CRO

| Observação | Interpretação | Implicação para a próxima onda |
|---|---|---|
| Oferta, galeria e contato estão em URLs diferentes. | O visitante precisa compor por conta própria a ligação entre serviço, prova visual e pedido de orçamento. | Arquitetar páginas de serviço com portfólio relacionado e CTA de orçamento. |
| O portfólio usa grupos técnicos e “Diversos”. | A taxonomia não é inteiramente orientada à necessidade de compra. | Aplicar taxonomia canônica do PRD internamente; publicar somente após HG-02. |
| A Home tem grande quantidade de imagens no HTML. | Há risco potencial de peso/competição de recursos, mas não houve medição de Core Web Vitals. | Fazer inventário, dedupe e QA de performance antes de conclusão. |
| O CTA registrado no diagnóstico do PRD é “Descubra mais”. | A chamada é menos explícita que uma ação de orçamento. | Validar CTA de orçamento como objetivo dominante da LP. |
| As marcas aparecem nos nomes do acervo. | Elas podem funcionar como contexto de projeto, não como prova automática de relacionamento. | Manter status de relacionamento/direitos como desconhecido até HG-01. |

## Hipótese operacional

Uma navegação que conecte cada serviço a imagens reais revisadas e a um CTA explícito de orçamento pode reduzir a necessidade de o visitante montar esse caminho entre páginas. Isso não foi medido e não deve ser tratado como melhoria até existir baseline e tracking validados.

## Lacunas / não verificado

- Não foram aferidos Lighthouse, CWV, responsividade visual, acessibilidade, console, tracking, envio/validação do formulário, nem funcionamento de WhatsApp para não produzir interação externa.
- Não foram capturados assets, hashes, dimensões, alt texts completos, duplicatas ou direitos; isso pertence ao inventário/curadoria da Wave 0.
- Não há confirmação de instalação, manutenção, prazos, quantidades mínimas, SLA, preço ou materiais por case.
- E-mails não são reproduzidos como dado editorial aprovado: o PRD pede validação e sinaliza possível artefato de texto em um endereço. [E-PRD §35]

## Ações recomendadas, sem execução de publicação

1. **Wave 0:** snapshot e inventário de URLs/assets, preservando originais e registrando hash/dedupe. [E-PRD §40]
2. **HG-01:** validar fatos que serão promovidos a copy (marcas, datas, serviços, materiais e qualquer informação operacional). [E-PRD §33]
3. **HG-02:** aprovar seleção hero, cases e classificação dos seis itens hoje agrupados como “Diversos”. [E-PRD §33]
4. **Wave 2:** desenhar routes, tracking e fonte de dados sem presumir conteúdo técnico ausente.

## Evidências

- **[E-LIVE-01]** GET público em `https://www.luminososargonbras.com/`, 2026-08-16: HTTP 200; HTML retornado com título, H1, links de contato e 36 `img` detectados.
- **[E-LIVE-02]** GET público em `https://www.luminososargonbras.com/servicos`, 2026-08-16: HTTP 200.
- **[E-LIVE-03]** GET público em `https://www.luminososargonbras.com/portfolio`, 2026-08-16: HTTP 200.
- **[E-LIVE-04]** GET público em `https://www.luminososargonbras.com/sobre`, 2026-08-16: HTTP 200.
- **[E-LIVE-05]** GET público em `https://www.luminososargonbras.com/contato`, 2026-08-16: HTTP 200.
- **[E-PRD]** PRD-fonte, §§1, 9–10, 33, 35, 40 e 52–53.
