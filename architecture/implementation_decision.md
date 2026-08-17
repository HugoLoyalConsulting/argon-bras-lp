# Decisão de implementação — Argon-Bras

**Decisão:** adotar uma arquitetura **static-first sem backend em runtime** para a primeira versão; gerar e publicar somente arquivos estáticos após aprovação humana.  
**Status:** aprovado para planejamento/implementação local; **não aprovado para publicação**.

## Evidência considerada

- O repositório declara uma “Landing page estática independente” no `README.md`.
- A raiz contém `index.html`, imagens locais e workflow de GitHub Pages; não há código-fonte de aplicação versionado, package manifest ou serviço de backend identificado.
- O export atual inclui resíduos de outro produto, inclusive URLs em `sitemap.xml` e `robots.txt`; ele é insuficiente como base de produção Argon-Bras.
- O PRD é stack-agnostic e exige performance, SEO, reutilização de LPs por serviço, portfólio, formulário e tracking, sem autorizar invenção de infraestrutura.

## Arquitetura alvo

```text
Conteúdo versionado e revisado
  ├─ services
  ├─ projects
  ├─ assets + metadados/evidências
  ├─ páginas + SEO
  └─ redirects
          ↓ build local/CI
HTML, CSS, imagens responsivas e JS progressivo
          ↓ artefato estático
Hospedagem estática (GitHub Pages ou destino aprovado)
```

### Decisões concretas

1. **Renderização:** pré-gerada no build; sem SSR, banco, autenticação ou API próprios nesta fase.
2. **Código:** reconstruir a fonte em diretório de source definido pelo Builder e tratar a raiz publicada como artefato. Preferir HTML semântico, CSS e JS mínimo; um gerador estático só é aceitável se sua cadeia de build for versionada, reprodutível e trouxer ganho claro de templates/dados.
3. **Conteúdo:** serviços, cases, assets e metadados em arquivos versionados, conforme `architecture/data_model.md`.
4. **Páginas:** Home, template de serviço, portfólio, case opcional, sobre, orçamento, privacidade e 404, conforme `architecture/site_map.md`.
5. **Mídia:** originais preservados; derivados AVIF/WebP/fallback responsivos; só LCP pré-carregado; restante lazy-loaded.
6. **Interação:** menu, filtros, FAQ e formulário com progressive enhancement; página continua navegável sem JavaScript onde aplicável.
7. **Formulário:** construir contrato e UI; **não habilitar submit, upload, página de obrigado ou promessa de confirmação** sem serviço de destino e HG-04. Como fallback, oferecer CTA de contato validado.
8. **Tracking:** pontos de instrumentação definidos, mas adaptador permanece ausente/no-op até escolha de ferramentas e HG-04. Não há analytics integrado nesta decisão.
9. **SEO:** metadados estáticos, sitemap, robots e redirects são gerados/atualizados apenas para domínio Argon-Bras aprovado. Corrigir os arquivos residuais antes do lançamento.
10. **Deploy:** nenhuma ação de push, deploy, DNS, Pages ou publicação é parte desta tarefa. O workflow existente pode publicar ao receber push em `main`; portanto, não fazer commit/push até o plano de release e HG-05.

## Por que static-first

| Critério do PRD | Resultado esperado |
|---|---|
| Performance | HTML pronto e mídia controlada reduzem custo de runtime |
| SEO | rotas e metadados legíveis no artefato final |
| Manutenção | conteúdo em arquivos, sem operação de banco/CMS para começar |
| Custo | hospedagem estática e ausência de backend contínuo |
| LPs por serviço | template + dados produzem rotas sem copiar markup |
| Portfólio | casos e ativos têm metadados auditáveis |
| Evolução | adaptadores explícitos permitem adicionar form/CRM/tracking depois |

## Opções descartadas agora

- **Reaproveitar o export atual como fonte:** rejeitado; é artefato insuficiente e contaminado por referências da Loyal Consulting.
- **CMS/headless desde o início:** adiado; não há requisito de edição não técnica ou credenciais/operador confirmados.
- **Backend customizado:** adiado; upload, lead e CRM ainda não têm contrato operacional ou requisitos de segurança aprovados.
- **Tags/pixels imediatos:** rejeitado até HG-04; evitar consentimento inadequado e coleta de PII.
- **Mudar de plataforma por preferência:** rejeitado; a solução deve ser avaliada contra deploy, domínio e governança aprovados.

## Plano de implementação por ondas

1. **Freeze/inventário:** snapshot, URLs, hashes, metadados e dedupe sem excluir originais.
2. **Conteúdo e gates:** validar claims, direitos, taxonomia, contatos, hero e seleção de cases.
3. **Fonte estática:** templates, dados, imagens otimizadas, SEO e redirects em ambiente local/preview não público.
4. **Integrações condicionais:** implementar form/tracking/consentimento apenas após HG-04 e review de segurança.
5. **QA:** acessibilidade, links, responsividade 360–1920px, Core Web Vitals, SEO, console e smoke de conversão.
6. **Release:** backup, staging, rollback, domínio e HG-05 antes de qualquer publicação.

## Human Gates e dependências

| Gate | Decisão humana necessária | Bloqueia |
|---|---|---|
| HG-01 | claims, serviços, materiais, contato, operação e marcas | conteúdo público |
| HG-02 | direitos/curadoria de assets e taxonomia | hero e portfólio |
| HG-03 | direção visual e DESIGN.md | UI final |
| HG-04 | ferramenta, privacidade, consentimento e destino de leads | form ativo, upload, tracking |
| HG-05 | release, domínio, redirects e rollback | produção |

## Critérios de saída da arquitetura

- Fonte/build estático reproduzível e separado do artefato publicado.
- Nenhuma referência residual a Loyal Consulting em conteúdo, sitemap, robots, metadata ou schema da entrega Argon-Bras.
- Dados desconhecidos permanecem `null`/ocultos.
- Nenhuma dependência de backend/analytics é alegada sem evidência de implementação.
- Sem publicação nesta fase.
