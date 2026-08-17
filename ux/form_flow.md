# Fluxo de formulário — Solicitar orçamento

## Objetivo e contrato

Converter interesse em um pedido **qualificado**, mas sem prometer preço, prazo, instalação, manutenção ou disponibilidade. O formulário é progressivo, acessível e compatível com LGPD; envio somente é considerado concluído após resposta confirmada do backend.

- **Rota:** `/orcamento`; CTAs podem pré-selecionar `service`, preservando a possibilidade de alterar.
- **Formato:** três etapas, uma decisão principal por tela no mobile; progresso textual “Etapa X de 3”.
- **Persistência:** manter dados no cliente durante a sessão e em retornos de validação. Persistência local além da sessão requer decisão de privacidade HG-04.
- **Dados técnicos invisíveis:** `lead_id` (após sucesso), UTMs, `gclid`, `fbclid`, landing page, referrer, first/last touch conforme arquitetura aprovada. Nunca enviar PII em analytics.

## Etapa 1 — O que você procura?

**Título:** “O que você procura?”  
**Ajuda:** “Escolha a opção mais próxima. Você poderá explicar o projeto depois.”

Seleção única obrigatória, com radios/tile controls semanticamente agrupados em `fieldset` e `legend`:

1. Letreiro luminoso
2. Backlight
3. Letras-caixa / logo 3D
4. Neon
5. Fachada / sinalização
6. Display / acrílico
7. Projeto especial
8. Não sei — quero orientação

| Campo | Requisito | Validação | Teclado/tipo |
|---|---|---|---|
| `service` | obrigatório | uma opção canônica | radios; setas e espaço |

**Ações:** `Continuar` (primária) e `Voltar` apenas quando veio de uma etapa anterior. Ao avançar, emitir `form_step_complete` com `form_step: 1`, serviço e página; não incluir dados pessoais.

## Etapa 2 — Seus dados

**Título:** “Como podemos falar com você?”  
**Ajuda:** “Usaremos estes dados para responder ao seu pedido.” Texto final de privacidade/uso deve ser validado no HG-04.

| Campo | Obrigatório | Tipo/autocomplete | Validação e erro útil |
|---|---:|---|---|
| Nome | sim | `text`, `name` | remover espaços; mínimo de caracteres definido pelo backend. “Informe seu nome para identificarmos o pedido.” |
| Empresa | não | `text`, `organization` | texto livre com limite seguro |
| WhatsApp | sim | `tel`, `tel-national`, teclado numérico | normalizar sem alterar a intenção; “Informe um WhatsApp com DDD.” |
| E-mail | sim | `email`, `email` | validação de formato; “Revise o formato do e-mail.” |
| Cidade / UF | sim | `text`, `address-level2` | cidade e UF legíveis; não geolocalizar sem consentimento |

- Labels persistentes; placeholders são apenas exemplos.
- “Opcional” aparece no label, não só no placeholder.
- `Continuar` valida client-side e server-side no envio; erro permanece associado com `aria-describedby` e `aria-invalid=true`.
- Ao voltar, nenhum dado é apagado.

## Etapa 3 — Conte sobre o projeto

**Título:** “Conte sobre o projeto”  
**Ajuda:** “Logo, referências, medidas aproximadas e uma foto do local ajudam a entender a necessidade.”

| Campo | Obrigatório | Comportamento |
|---|---:|---|
| Descrição | sim | textarea; orientar contexto/objetivo sem exigir vocabulário técnico |
| Logo | não | upload controlado; formatos e limite só são exibidos após definição técnica/segurança |
| Foto do local | não | upload controlado; mesmos limites definidos no backend |
| Referências | não | upload ou campo de link **somente** se a capacidade estiver implementada; não desenhar promessa vazia |
| Medidas aproximadas | não | texto livre curto; não calcular preço |
| Consentimento/privacidade | conforme decisão jurídica | link de privacidade e linguagem aprovada no HG-04 |

Ações: `Voltar` (secundária) e `Solicitar orçamento` (primária). O botão tem estado loading, é desabilitado contra duplo envio e conserva foco/feedback textual.

## Máquina de estados

```text
idle
  → editing
  → client-validating
  → invalid (campos com erro; valores preservados)
  → submitting
      → success (backend confirma lead_id)
      → server-validation-error (campos mapeados)
      → upload-error (arquivo permanece/retry possível)
      → network-error (nenhum sucesso declarado; retry)
```

| Estado | UI | A11y | Analytics |
|---|---|---|---|
| loading | botão com texto “Enviando pedido…”, spinner secundário | `aria-live="polite"`; não remover rótulo | não emitir `generate_lead` |
| server validation | resumo no topo + mensagem por campo | foco no resumo, links para campos | `form_error` sem PII |
| upload progress | nome, percentual e remover/tentar novamente | progresso nomeado | `form_upload` com tipo/resultado, sem nome do arquivo |
| network error | “Não foi possível enviar agora. Seus dados continuam nesta página.” + Tentar novamente | anúncio assertivo moderado | `form_error` com código técnico seguro |
| success | título “Recebemos seu pedido”, lead ID se disponível, próximo passo **somente confirmado** | foco no H1/landmark de confirmação | `generate_lead`, depois `thank_you_view` |

## Pós-envio

1. Backend retorna resposta explícita de sucesso, `lead_id` e somente dados seguros para UI.
2. Disparar `generate_lead` uma vez, protegido por idempotency key/estado da submissão.
3. Navegar ou trocar para thank-you acessível; preservar atribuição no servidor, não em query string com PII.
4. Não prometer prazo de retorno; usar “Entraremos em contato pelos dados informados” somente se operação confirmar.
5. CTA WhatsApp no sucesso só aparece se o canal e a mensagem forem aprovados; é alternativa, não alegação de que o formulário chegou ao WhatsApp.

## Eventos mínimos

| Evento | Quando | Parâmetros permitidos |
|---|---|---|
| `form_start` | primeira interação qualificada | `service`, `placement`, `page_type`, `landing_page` |
| `form_step_complete` | avanço válido em cada etapa | `form_step`, `service` |
| `form_upload` | tentativa/conclusão/falha de upload | `form_step`, `upload_type`, `result` |
| `form_error` | erro client/server/upload/rede | `form_step`, `field_name`, `error_type` |
| `generate_lead` | sucesso confirmado uma única vez | `service`, `landing_page`, `campaign`, `source`, `medium` |

## Requisitos de implementação e QA

- HTML nativo (`form`, `label`, `fieldset`, `legend`, `button`) antes de ARIA adicional.
- `inputmode` correto: `tel` para WhatsApp, `email` para e-mail; não bloquear colar.
- Tap targets ≥44 px (recomendado 52 px para campo/botão); zoom a 200% não perde controles.
- Upload: MIME allowlist, extensão, tamanho, malware scan/armazenamento e retenção definidos por Security/Reliability antes de ativar. Se não houver suporte real, ocultar upload — não usar mock.
- Proteção antispam/rate limit e tratamento de timeout são pré-condições de produção.
- Testar: campos obrigatórios, formato de e-mail/WhatsApp, teclado, back/forward, recuperação de rede, um único `generate_lead`, UTM, upload permitido/negado e leitor de tela.

## Human Gates

- **HG-01:** serviços, processo e qualquer promessa de contato/prazo.
- **HG-04:** texto de privacidade, retenção, ferramentas de analytics, atribuição e tratamento de uploads.
- **HG-05:** teste end-to-end HTTPS → API → persistência/CRM antes de afirmar que o form está operacional.
