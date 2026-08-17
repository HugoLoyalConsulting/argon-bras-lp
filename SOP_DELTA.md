# SOP_DELTA — Wave 1: Research + Market Validation

```yaml
sop_id: SOP-LP-001 / SOP-LP-005 / SOP-LP-006 / SOP-LP-007 / SOP-LP-019
author: Opportunity Researcher + Market Validator
task_id: W1-01
date: 2026-08-16
sop_version_used: PRD_ARGON_BRAS_LP_HIGH_CALIBER.md v1.0
status: proposed_for_review
what_worked:
  - A separação explícita de fato, interpretação e hipótese no PRD permitiu produzir pesquisa sem transformar recomendações em claims.
  - As cinco URLs públicas Argon listadas no PRD foram suficientes para confirmar disponibilidade pública das superfícies e delimitar a auditoria sem fontes externas.
what_failed:
  - Não havia Search Console, analytics, CRM, dados de mercado, concorrentes ou metadados de assets entre as fontes permitidas; portanto, não foi possível validar demanda, benchmark competitivo, conversão ou direitos por imagem.
new_pattern:
  - Para sites com acervo público, registrar cada afirmação em uma matriz Fato → Fonte → Condição de uso editorial antes de propor copy ou prova social.
  - Tratar nomes de marcas no portfólio como contexto de asset, não como relacionamento comercial, até gate factual.
anti_pattern:
  - Inferir que uma marca nomeada no portfólio é cliente/parceira.
  - Converter ano de início em idade empresarial sem data completa.
  - Usar volume de imagens como número de projetos, clientes ou prova de escala.
new_check:
  - Toda proposta de valor deve incluir: fato fonteado, necessidade interpretada, proposta candidata, prova permitida, proibições e gate necessário.
  - Todo mapa de intenção sem dados de busca deve ser rotulado como hipótese e deve listar os dados necessários para validação.
tool_notes:
  - Consultas HTTP públicas confirmaram HTTP 200 para Home, Serviços, Portfólio, Sobre e Contato em 2026-08-16; nenhuma interação de formulário ou publicação foi realizada.
  - O parser HTML sem biblioteca especializada gerou saída ruidosa em links devido ao HTML do provedor; usar extração estruturada/snapshot na Wave 0 para inventário de assets, não essa saída como inventário final.
decision_rule:
  - Se uma afirmação não puder ser ancorada no PRD ou em uma URL pública Argon listada, classificá-la como hipótese/TBD ou removê-la. Não preencher por plausibilidade.
evidence:
  - research/evidence_pack.md
  - research/current_site_audit.md
  - research/search_intent_map.md
  - validation/value_prop_matrix.md
  - validation/message_hypotheses.md
  - validation/risk_register.md
recommended_change:
  - Incorporar o checklist Fato → Fonte → Condição de uso editorial aos SOPs de auditoria, social proof, hero e experimentos antes de qualquer build.
confidence: alta para o padrão de controle de alegações; baixa para qualquer inferência de demanda ou desempenho sem dados adicionais
review_required: true
reviewers:
  - Owner comercial para HG-01
  - Curadoria/owner para HG-02
  - Product Analytics/privacidade para HG-04
```

## Nota factual de escopo

Este delta registra um aprendizado real: o PRD contém material suficiente para formar uma arquitetura de hipóteses e limites editoriais, mas não para demonstrar demanda, concorrência, performance ou relacionamento com marcas. A recomendação é atualizar SOPs, não publicar qualquer alteração.
