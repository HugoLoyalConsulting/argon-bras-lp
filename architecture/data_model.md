# Modelo de dados — Argon-Bras

**Status:** modelo de conteúdo estático; não há banco de dados, CMS ou API confirmados.  
**Objetivo:** permitir gerar páginas de serviço, portfólio e formulário sem inferir fatos ausentes.

## Estratégia static-first

A fonte de verdade inicial são arquivos versionados (YAML, JSON ou Markdown com frontmatter), revisados por pull request e compilados para HTML estático. O modelo deve poder migrar para CMS/headless depois sem mudar os contratos de campos.

`null` significa “desconhecido/não confirmado” e deve resultar em omissão na UI. Nunca preencher com estimativa plausível.

## Entidades de conteúdo

### Service

```yaml
id: illuminated_sign
slug: letreiros-luminosos
title: Letreiros luminosos
summary: null                 # publicar apenas após aprovação de copy
service_category: illuminated_sign
subcategories: [frontlit]     # somente categorias aprovadas
applications: []
materials: []                 # somente materiais aplicáveis e confirmados
hero_asset_id: null
featured_project_ids: []
seo:
  title: null
  description: null
  canonical_path: /letreiros-luminosos/
publish_status: draft         # draft | approved | published | archived
evidence: []
data_confidence: unverified   # unverified | partial | confirmed
```

### Project (case do portfólio)

```yaml
id: project-0001
slug: null
title: null
brand_display_name: null
client_relationship_status: unknown # unknown | portfolio_reference | approved_client_claim
service_category: null
service_subcategory: null
application: null
materials: []
lighting_type: null
city: null
state: null
year: null
summary: null
technical_description: null
cover_asset_id: null
gallery_asset_ids: []
featured: false
hero_eligible: false
seo:
  title: null
  description: null
alt_text: null
source_url: null
evidence: []
data_confidence: unverified
rights_status: unknown        # unknown | review_required | approved_for_site | restricted
publish_status: draft
```

**Regra de marca:** `brand_display_name` prova que a marca aparece no acervo, não que é cliente, parceiro ou endossante. Essa alegação requer `client_relationship_status: approved_client_claim` e HG-01/HG-02.

### Asset

```yaml
asset_id: asset-0001
source_page: null
source_url: null
original_filename: null
original_alt: null
original_heading_context: null
original_path: /images/argon/source-original/example.jpg
normalized_path: null
optimized:
  avif: []
  webp: []
  fallback: []
width: null
height: null
mime_type: null
bytes: null
sha256: null
perceptual_hash: null
duplicate_group: null
project_id: null
service_category: null
application_category: null
brand_or_project: null
quality_score: null
hero_eligible: false
featured: false
rights_status: unknown
migration_status: inventoried # inventoried | normalized | optimized | approved | excluded
notes: null
```

Originais são imutáveis; versões normalizadas/otimizadas são derivadas. Deduplicação exata usa SHA-256 e near-duplicate usa perceptual hash, ambos seguidos de revisão humana para crops/edições.

### PageMeta

```yaml
path: /
title: null
description: null
canonical_path: /
og_image_asset_id: null
robots: index,follow
schema_types: []
publish_status: draft
```

### Redirect

```yaml
from_path: null
to_path: null
status_code: 301
reason: migration
verified: false
```

Não criar redirecionamento até o inventário de URLs do site atual e o domínio de destino serem aprovados.

## Captura de lead — contrato futuro, não persistência atual

O site estático não mantém leads. Caso o HG-04 aprove uma integração, o adaptador de formulário poderá enviar este contrato ao destino autorizado:

```yaml
lead_id: null                 # gerado pelo serviço de destino, nunca no cliente como fonte de verdade
service_interest: null
name: null
company: null
whatsapp: null
email: null
city_uf: null
project_description: null
approximate_measurements: null
reference_url: null
attachments: []               # somente após upload seguro aprovado
attribution:
  utm_source: null
  utm_medium: null
  utm_campaign: null
  utm_content: null
  utm_term: null
  gclid: null
  fbclid: null
  landing_page: null
  referrer: null
  first_touch: null
  last_touch: null
consent:
  policy_version: null
  captured_at: null
```

- PII não entra em URLs, data layer público, logs de console ou analytics.
- Capturar e reter apenas campos, prazo e base legal aprovados pela revisão de privacidade.
- Sem backend aprovado, o formulário deve indicar caminho alternativo seguro (por exemplo, contato direto) em vez de fingir envio.

## Taxonomias canônicas

```text
SERVICE: illuminated_sign > frontlit | backlit; dimensional_lettering; neon;
         facade_signage; display_acrylic; special_project
APPLICATION: facade; indoor; retail; corporate; stand_event; automotive;
             hospitality; industrial; other
```

A categoria histórica “Diversos” é apenas fonte de migração; não é taxonomia pública. Cada remapeamento exige confiança e revisão humana.

## Integridade e publicação

Um projeto só é elegível à página pública quando: `slug`, `title`, `cover_asset_id`, `service_category`, `alt_text`, `rights_status: approved_for_site`, `publish_status: approved` e evidência correspondente estiverem presentes. Campos opcionais não confirmados continuam `null` e não aparecem.

## Dependências e Human Gates

- Inventário de assets, hashes e source URLs.
- HG-01 para fatos e descrições; HG-02 para direitos, seleção e taxonomia; HG-04 para dados de lead/atribuição.
- Ferramenta de build estático e convenção de arquivos escolhidas pelo Builder, mantendo este contrato.
