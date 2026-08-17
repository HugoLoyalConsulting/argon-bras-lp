# Mapa de componentes — Argon-Bras

**Status:** contrato de implementação; não implementado.  
**Princípio:** componentes estáticos, acessíveis e reutilizáveis. JavaScript é progressivo e só é incluído quando melhora uma interação real.

## Camadas

```text
Dados estáticos validados
        ↓
Templates de página (Home, Serviço, Portfólio, Case, Institucional, Orçamento)
        ↓
Seções reutilizáveis
        ↓
Primitivos semânticos (links, botões, mídia, heading, field)
```

A primeira entrega pode ser HTML/CSS/JS estático organizado em parciais ou em gerador estático. Não pressupõe React, CMS, API ou rendering no servidor.

## Shell global

| Componente | Responsabilidade | Dados / estados | Reuso |
|---|---|---|---|
| `SiteHeader` | logo, navegação e CTA primário | menu aberto/fechado em mobile; foco e Escape | todas as páginas |
| `MobileNav` | navegação compacta acessível | aberto, fechado, foco preso somente se modal | todas as páginas |
| `StickyBudgetCTA` | CTA inferior após hero no mobile | oculto antes/depois conforme UX aprovada | Home e LPs |
| `SiteFooter` | contatos validados, links legais e navegação secundária | dados de contato aprovados | todas as páginas |
| `SkipLink` | salto para conteúdo principal | foco por teclado | todas as páginas |
| `SeoHead` | title, description, canonical, OG e robots | metadados de rota aprovados | build-time |

## Seções de conteúdo e conversão

| Componente | Contrato | Restrições e dados exigidos |
|---|---|---|
| `Hero` | eyebrow, H1, texto curto, imagem LCP, CTA primário e secundário | uma imagem real aprovada; máximo dois CTAs; sem slideshow automático |
| `AuthorityStrip` | fatos curtos de autoridade | só afirmações aprovadas; marcas não são “clientes” sem autorização |
| `ServiceMatrix` | mosaico editorial de famílias comerciais | dados de `Service`; não usar grade genérica de cards nem “Diversos” público |
| `ServiceCard` | imagem, título, resumo e links de serviço/orçamento | imagem e copy aprovadas; metadados não confirmados ocultos |
| `FeaturedWork` | seleção de 6–8 cases | somente `publish_status: approved`; direitos revisados |
| `PortfolioGrid` | grade de projetos com carga progressiva | `Project` e `Asset`; evita carregar galeria inteira de início |
| `PortfolioFilters` | filtros por serviço e aplicação | comportamento JS opcional; deve degradar para links/visão completa |
| `CaseSpotlight` | destaque editorial de um case | tipo/aplicação somente se confirmados |
| `CaseDetail` | título, mídia, atributos e CTA | omite campos `null`; não cria descrição técnica inferida |
| `ProcessSteps` | etapas do fluxo comercial | instalação/entrega só com operação confirmada |
| `ApplicationsList` | segmentos onde há evidência | cada segmento requer evidência ou confirmação |
| `FaqAccordion` | perguntas e respostas | HTML semântico; resposta operacional validada; não publicar FAQ especulativa |
| `FinalCTA` | chamada final para orçamento e WhatsApp | link/telefone validados; não promete retorno/prazo |

## Formulário e integrações — contratos, não funcionalidades existentes

| Componente | Estado previsto | Condição de ativação |
|---|---|---|
| `BudgetForm` | UI em etapas: serviço, contato, projeto | destino de lead, LGPD, antispam e validação aprovados |
| `FormField` | label, ajuda, erro associado e input | sempre acessível; sem PII em atributos de tracking |
| `FileUpload` | opcional: logo/foto do local | desabilitado/removido até existir armazenamento seguro, limites, antivírus e política |
| `FormSubmissionAdapter` | fronteira abstrata de envio | inexistente nesta fase; implementar apenas com endpoint/provedor aprovado |
| `SubmissionStatus` | loading, erro, sucesso | `/obrigado/` somente após submissão real bem-sucedida |
| `WhatsAppCTA` | link externo configurável | URL e mensagem aprovadas; tracking somente após HG-04 |
| `TrackingAdapter` | despacho de eventos sem PII | **não integrado**; pode ser no-op até ferramenta e consentimento aprovados |
| `ConsentManager` | lê/grava preferência de consentimento | não implementar sem decisão jurídica e ferramenta definida |

## Primitivos e requisitos transversais

- `Button` distingue navegação (`<a>`) de ação (`<button>`); alvo mínimo de 44×44 px.
- `ResponsiveImage` exige `alt`, dimensões/aspect ratio, `srcset` e `loading="lazy"` fora do LCP; preserva original no acervo.
- `Section` mantém hierarquia de headings e largura editorial.
- `Dialog`/menu/accordion funcionam por teclado, têm foco visível e respeitam `prefers-reduced-motion`.
- Todo CTA tem `placement`, `label`, `target` e `service` opcionais para futura telemetria; isso não significa que o evento já seja enviado.

## Composição por template

```text
Home: SiteHeader → Hero → AuthorityStrip → ServiceMatrix → FeaturedWork
      → CaseSpotlight → ProcessSteps → ApplicationsList → FAQ → BudgetForm → FinalCTA → SiteFooter

Serviço: SiteHeader → Hero específico → AuthorityStrip → prova filtrada
         → opções técnicas aprovadas → PortfolioGrid → ProcessSteps → FAQ específico → BudgetForm → SiteFooter

Portfólio: SiteHeader → intro → PortfolioFilters → PortfolioGrid → FinalCTA → SiteFooter

Case: SiteHeader → CaseDetail → projetos relacionados → FinalCTA → SiteFooter
```

## Dependências / Human Gates de componente

- `Hero`, `FeaturedWork`, `CaseSpotlight` e `PortfolioGrid`: HG-02.
- Copy de serviços, FAQ e `ProcessSteps`: HG-01.
- Tokens, composição e motion: HG-03.
- `BudgetForm`, `FileUpload`, `TrackingAdapter`, `ConsentManager`: HG-04.
- `SeoHead` com domínio final, sitemap e publicação: HG-05.
