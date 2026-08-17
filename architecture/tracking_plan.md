# Plano de tracking e mensuração — Argon-Bras

**Status:** especificação de instrumentação. **Nenhuma ferramenta de analytics, pixel, CAPI, CRM, armazenamento de UTM ou evento está confirmada como integrada no repositório.**

## Objetivo e limites

Mensurar o funil de orçamento sem coletar PII em plataformas de analytics e sem ativar terceiros antes de aprovação de privacidade. A North Star proposta é **solicitação de orçamento qualificada**, mas a qualificação depende de operação/CRM ainda não definido.

Até HG-04, o site deve funcionar sem analytics: não incluir IDs, SDKs, pixels, scripts de tag manager ou alegar que eventos são enviados.

## Plano por fases

| Fase | Resultado | Pré-requisito | Estado |
|---|---|---|---|
| 0 — contrato | dicionário abaixo e pontos de instrumentação documentados | nenhum | definido neste arquivo |
| 1 — decisão | ferramenta(s), contas, proprietários, consentimento e retenção aprovados | HG-04 | pendente |
| 2 — implementação | adaptador de tracking e consentimento, sem PII | Fase 1 | pendente |
| 3 — QA | DebugView/teste de tags, deduplicação e consentimento | ambiente de staging | pendente |
| 4 — baseline | relatório pós-lançamento e backlog CRO | produção aprovada (HG-05) | pendente |

## Eventos propostos

| Evento | Disparo | Parâmetros permitidos | Não enviar |
|---|---|---|---|
| `page_view` | visualização de rota | `page_type`, `path`, campanha não-PII | nome, e-mail, telefone, descrição |
| `view_service` | seção/página de serviço visível ou aberta | `service`, `placement`, `page_type` | PII |
| `view_portfolio_item` | card/case aberto | `project`, `service`, `placement` | PII |
| `portfolio_filter` | filtro aplicado | `filter_type`, `filter_value` | PII |
| `cta_click` | CTA interno | `placement`, `cta_label`, `target`, `service`, `cta_variant` | PII |
| `whatsapp_click` | link WhatsApp acionado | `placement`, `service`, `page_type` | texto da conversa, telefone |
| `phone_click` / `email_click` | link correspondente acionado | `placement`, `page_type` | valor do contato em eventos |
| `form_start` | primeira interação do formulário | `service`, `form_id`, `page_type` | valores de campo |
| `form_step_complete` | etapa válida concluída | `form_id`, `form_step`, `service` | valores de campo |
| `form_upload` | arquivo aceito para envio | `form_id`, `form_step`, `file_type` | nome, conteúdo e URL do arquivo |
| `form_error` | falha de validação/submissão | `form_id`, `form_step`, `error_code` | texto digitado |
| `generate_lead` | serviço de destino confirma recepção | `lead_id` pseudônimo/servidor, `service`, atribuição permitida | PII e anexos |
| `thank_you_view` | página de confirmação exibida após sucesso real | `form_id`, `service` | PII |
| `faq_open` | item FAQ expandido | `faq_id`, `page_type` | PII |
| `scroll_50` / `scroll_90` | primeiro alcance do marco por página | `page_type`, `path` | PII |

Eventos são intenções/telemetria; `whatsapp_click` não equivale a conversa iniciada nem a lead qualificado.

## Parâmetros normalizados

| Parâmetro | Convenção |
|---|---|
| `service` | ID canônico de `Service` |
| `project` | slug/ID público do case, nunca dado privado |
| `placement` | `hero`, `header`, `sticky_mobile`, `service_card`, `case`, `form`, `footer` |
| `page_type` | `home`, `service`, `portfolio`, `case`, `about`, `budget`, `legal` |
| `cta_variant` | versão aprovada, ausente se não há experimento |
| `form_step` | `service`, `contact`, `project`, `submit` |
| `campaign`, `source`, `medium` | atribuição normalizada, somente após aprovação |

## Atribuição e privacidade

Atribuição desejada: `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term`, `gclid`, `fbclid`, `landing_page`, `referrer`, `first_touch` e `last_touch`.

- Implementar persistência somente após base legal, texto de privacidade, prazo de retenção e mecanismo de consentimento aprovados.
- Nunca anexar PII a UTMs, URLs, eventos ou identificadores publicitários.
- `gclid`/`fbclid` devem ser tratados como dados de atribuição e revisados pelo jurídico.
- Server-side/CAPI só será considerado se houver endpoint seguro, segredo protegido, contrato de deduplicação e revisão de segurança. Não fazem parte da entrega estática inicial.

## QA obrigatório antes de ativar

1. Validar que cada CTA emite no máximo um evento por ação.
2. Confirmar que recusa/ausência de consentimento bloqueia tags conforme política aprovada.
3. Inspecionar payloads: zero PII, anexos, textos de formulário ou URLs privadas.
4. Testar navegação, filtros, WhatsApp, erros e sucesso em mobile e desktop.
5. Validar `generate_lead` somente contra submissão aceita pelo destino; não ao clicar em enviar.
6. Registrar evidência de ferramenta (DebugView/tag assistant/log de endpoint) no relatório de analytics.

## Dependências e Human Gates

- **HG-04:** decisão de GA4/Ads/Meta/outro, contas, consentimento e privacidade.
- Destino operacional de lead para `generate_lead` e retenção de atribuição.
- HG-05 e domínio final para baseline de produção.
- Volume e métricas definidas antes de qualquer experimento A/B.
