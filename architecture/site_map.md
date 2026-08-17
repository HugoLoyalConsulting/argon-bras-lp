# Mapa do site — Argon-Bras

**Status:** arquitetura proposta; não implementada nem publicada  
**Fonte:** PRD Argon-Bras v1.0 (16/08/2026) e inspeção do repositório em 16/08/2026.

## Decisão de escopo

A experiência será **static-first, portfolio-led e orientada a orçamento**. As páginas são conteúdo estático pré-gerado e não dependem de backend em tempo de execução. Serviço, portfólio e formulário são previstos como capacidades, mas nenhuma integração de envio, CRM, analytics ou consentimento é assumida como existente.

A raiz atual do repositório é um export estático e contém referências residuais a outro produto nos arquivos `sitemap.xml` e `robots.txt`; ele **não é fonte canônica** para as rotas abaixo e deve ser substituído somente após os Human Gates.

## Rotas canônicas propostas

| Rota | Tipo | Objetivo / conteúdo | Estado nesta arquitetura |
|---|---|---|---|
| `/` | Home/LP | proposta, prova visual, famílias de serviço, trabalhos destacados, processo, FAQ e CTA de orçamento | P0 |
| `/letreiros-luminosos/` | LP de serviço | iluminação frontal, letras-caixa iluminadas e logotipos luminosos | P0 template; conteúdo sujeito a HG-01/02 |
| `/backlight/` | LP de serviço | iluminação traseira/indireta | P0 template; conteúdo sujeito a HG-01/02 |
| `/letras-caixa/` | LP de serviço | letras e logotipos 3D, iluminados ou não quando confirmado | P0 template; conteúdo sujeito a HG-01/02 |
| `/neon/` | LP de serviço | neon personalizado | P0 template; conteúdo sujeito a HG-01/02 |
| `/fachadas-sinalizacao/` | LP de serviço | fachadas e sinalização | P0 template; conteúdo sujeito a HG-01/02 |
| `/displays-acrilico/` | LP de serviço | PETG, displays, acrílico e luminárias somente conforme evidência | P0 template; conteúdo sujeito a HG-01/02 |
| `/projetos-especiais/` | LP de serviço | aplicações fora das famílias anteriores; não expõe “Diversos” | P0 template; curadoria necessária |
| `/portfolio/` | Índice | grade filtrável por serviço e aplicação; prova visual antes de descrição | P0 |
| `/portfolio/{slug-case}/` | Case estático | metadados confirmados, galeria e CTA contextual | P1; gerar apenas cases aprovados |
| `/sobre/` | Institucional | história desde 1987, localização e atuação somente como confirmadas | P0 |
| `/orcamento/` | Conversão | formulário progressivo e alternativa WhatsApp; sem falsa confirmação de envio | P0 UI; ativação depende de HG-04 e integração |
| `/privacidade/` | Legal | dados coletados e terceiros efetivamente usados | P0 antes de coletar PII |
| `/cookies/` | Legal condicional | preferências/consentimento, apenas se ferramentas/cookies exigirem | condicional |
| `/obrigado/` | Conversão | confirmação pós-envio; só publicar se o fluxo de envio estiver funcional | condicional |
| `/404.html` | Resiliência | rota inexistente com retorno à Home e orçamento | P0 |

## Rotas futuras — não criar sem demanda e conteúdo aprovado

- `/letreiros-luminosos/{segmento}/`
- `/neon/{segmento}/`
- `/fachadas-sinalizacao/{segmento}/`

Essas LPs herdam o template de serviço. Cada uma exige: intenção/campanha definida, prova visual relevante, copy aprovada e metadados SEO próprios. Não são simples duplicações de texto.

## Navegação e conversão

```text
Home
 ├─ Serviços → LP específica → portfólio filtrado → orçamento/WhatsApp
 ├─ Portfólio → case → serviço relacionado → orçamento/WhatsApp
 ├─ Sobre → orçamento/WhatsApp
 └─ CTA persistente → /orcamento/ ou link WhatsApp validado
```

- Header desktop: Serviços, Portfólio, Sobre e CTA **Solicitar orçamento**.
- Mobile: menu compacto, CTA visível e CTA inferior sticky após o hero.
- Cada LP mantém um objetivo dominante: solicitar orçamento.
- WhatsApp é uma saída de conversão; o número, a mensagem pré-preenchida e a disponibilidade devem ser validados antes da publicação.

## SEO, indexação e migração

1. Gerar `sitemap.xml`, `robots.txt`, canonicals e metadados a partir do domínio de produção **aprovado** — não reutilizar URLs da Loyal Consulting.
2. Antes do cutover, inventariar URLs atuais, definir redirecionamentos 301 antigo→novo e validar propriedade do domínio/DNS.
3. Não indexar `/obrigado/` nem ambientes de preview.
4. Só emitir schema.org quando dados empresariais, serviços e elegibilidade forem aprovados; sem reviews, clientes ou métricas inventados.
5. Preservar os originais de ativos e a relação origem→novo uso; não apagar acervo durante a migração.

## Dependências e Human Gates

| Dependência / gate | Necessário para | Responsável humano |
|---|---|---|
| HG-01 — claims factuais | textos de serviços, datas, materiais, atendimento, instalação, prazos e marcas | Argon-Bras |
| HG-02 — curadoria de portfólio | hero, cases destacados, classificação de “Diversos”, direitos de imagem/marca | Argon-Bras |
| HG-03 — direção visual | construção integral de UI e recortes finais | Argon-Bras / Brand |
| HG-04 — tracking e privacidade | qualquer tag, cookie, UTM persistido, formulário com PII ou link de conversão mensurado | Argon-Bras / jurídico |
| HG-05 — release | substituição do export atual, DNS/Pages e indexação | Argon-Bras / responsável de release |
| Inventário e deduplicação | publicação de portfólio e seleção de hero | Creative + revisão humana |
| Destino operacional do lead | ativar formulário e página de obrigado | Operação comercial |

## Fora de escopo agora

E-commerce, orçamento automático, CMS/headless, CRM, upload persistente, A/B testing, personalização e multilingual. Eles podem ser adicionados apenas quando houver necessidade e infraestrutura aprovada.
