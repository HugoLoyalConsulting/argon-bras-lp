# Evidence Pack — Wave 1

**Projeto:** Argon-Bras LP
**Status:** evidência reunida; pronta para handoff a Product Architecture, UX e curadoria.
**Regra:** fatos possuem fonte; interpretações não são fatos; hipóteses não são resultado.

## Registro de fontes permitidas e usadas

| ID | Fonte | Escopo utilizado | Observação |
|---|---|---|---|
| E-PRD | PRD-fonte preservado em `/root/.hermes/profiles/gerenciabrica_bot/cache/documents/doc_7c0b41977a28_PRD_ARGON_BRAS_LP_HIGH_CALIBER.md` | Contexto, inventário de serviços/portfólio, regras, gates e recomendações | Fonte primária do projeto; cópia de ponte em `00-admin/PRD.md`. |
| E-SITE-HOME | https://www.luminososargonbras.com/ | Oferta, histórico declarado, navegação/contato público | Consulta técnica pública em 2026-08-16 (HTTP 200). |
| E-SITE-SERVIÇOS | https://www.luminososargonbras.com/servicos | Serviços e materiais declarados | Consulta técnica pública em 2026-08-16 (HTTP 200). |
| E-SITE-PORTFOLIO | https://www.luminososargonbras.com/portfolio | Nomes/grupos de portfólio via inventário do PRD | Consulta técnica pública em 2026-08-16 (HTTP 200). |
| E-SITE-SOBRE | https://www.luminososargonbras.com/sobre | Superfície institucional existente | Consulta técnica pública em 2026-08-16 (HTTP 200). |
| E-SITE-CONTATO | https://www.luminososargonbras.com/contato | Canais de contato e formulário | Consulta técnica pública em 2026-08-16 (HTTP 200). |

## Fatos utilizáveis na próxima etapa

| ID | Fato | Fonte | Condição de uso editorial |
|---|---|---|---|
| F-01 | O site declara atuação em comunicação visual, letreiros, neons, luminosos, fachadas e displays. | E-SITE-HOME; E-PRD §52 | Pode ser usado como descrição de oferta; manter redação compatível com o site. |
| F-02 | O site declara “Desde 1987”. | E-SITE-HOME; E-PRD §53 | Pode usar “desde 1987”; não derivar contagem de anos. |
| F-03 | Serviços descreve letras-caixa frontal, traseira ou sem iluminação. | E-SITE-SERVIÇOS; E-PRD §1.1 | Pode descrever as três variações. |
| F-04 | Serviços cita chapa galvanizada pintada, inox, PVC expandido, acrílico e latão para letras/logotipos. | E-SITE-SERVIÇOS; E-PRD §1.1 | Não atrelar material a case sem evidência de case. |
| F-05 | Serviços apresenta Neon, Bandeja/Display em PETG e Luminárias em Acrílico. | E-SITE-SERVIÇOS; E-PRD §1.1 | Não expandir para instalação, manutenção, prazo ou volume. |
| F-06 | O PRD inventaria 38 imagens nomeadas em cinco grupos. | E-PRD §10 | Não tratar como 38 projetos/clientes; são imagens nomeadas. |
| F-07 | O portfólio contém itens com nomes de marcas/projetos, incluindo Samsung, Honda, Mitsubishi, Porsche, Mercedes-Benz, Ambev, Bradesco e outros. | E-PRD §§0, 10 | Usar somente como “trabalhos registrados no portfólio” até HG-01. |
| F-08 | Contato publica telefone/WhatsApp, e-mails, Instagram, endereço e formulário de orçamento. | E-SITE-CONTATO; E-PRD §52 | Validar contatos antes de republicar. |
| F-09 | O PRD define solicitação de orçamento qualificada como North Star e WhatsApp/formulário como macroconversões. | E-PRD §2.3–2.4 | É direção de produto, não métrica corrente. |

## Interpretações registradas

| ID | Interpretação | Base | Decisão que suporta |
|---|---|---|---|
| I-01 | O acervo está subaproveitado quando separado da oferta e apresentado primordialmente como galeria. | Diagnóstico do PRD §1.2 | Arquitetura portfolio-led. |
| I-02 | “Diversos” é uma categoria fraca para decisão/SEO. | PRD §1.2, §11 | Retaxonomizar com revisão humana. |
| I-03 | Serviço específico + prova relacionada + CTA explícito forma um caminho comercial mais claro que páginas isoladas. | PRD §§5 e 7 | Template de LP por serviço. |
| I-04 | O histórico declarado e a variedade de técnicas são provas mais seguras que superlativos. | F-02 a F-05; PRD §7.9 | Copy direta, sem métricas inventadas. |

## Hipóteses formalizadas

| ID | Hipótese | Medida necessária antes de concluir | Pré-condições |
|---|---|---|---|
| H-01 | Prova visual cedo e CTA persistente elevam cliques para WhatsApp/orçamento. | `cta_click`, `whatsapp_click`, `form_start`, `generate_lead` | Tracking validado; baseline. |
| H-02 | Formulário em etapas reduz atrito versus formulário único. | início, conclusão, erro e abandono por etapa | Instrumentação e experimento controlado. |
| H-03 | LPs por serviço melhoram message match de campanhas. | origem/campanha, landing, serviço, conversão qualificada | UTMs, definição de lead qualificado. |
| H-04 | Cases contextualizados aumentam confiança percebida. | Pesquisa qualitativa e progressão no funil | Cases e direitos aprovados. |

## Pontos bloqueados para Human Gate

| Gate | Item | Motivo |
|---|---|---|
| HG-01 factual claims | Marcas como clientes/parceiros; datas derivadas; instalação; manutenção; prazo; quantidade mínima; materiais por projeto | Não há evidência suficiente nas fontes permitidas. |
| HG-02 portfolio curation | Hero, cases, qualidade/direitos e classificação de “Diversos” | Exigem inspeção/decisão humana por asset. |
| HG-04 tracking/privacy | Ferramentas de analytics e consentimento | PRD exige aprovação antes da ativação. |
| HG-05 production release | Qualquer publicação externa | Fora do escopo desta Wave e vedado sem gate. |

## Handoff factual

- **Para Architecture:** usar F-01–F-09 como limites de conteúdo; campos desconhecidos devem permanecer `null`/TBD.
- **Para UX/UI:** priorizar entendimento da oferta, prova real e orçamento; não usar marcas como selo de confiança sem HG-01.
- **Para Creative/Wave 0:** inventariar e revisar assets antes de selecionar hero/cases; preservar originais.
- **Para Growth/Analytics:** não definir meta de conversão com benchmark externo; criar baseline próprio conforme PRD.
