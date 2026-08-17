# Execution status — Argon-Bras LP refactor

> Fonte operacional versionável. Atualizado em 2026-08-16.

## Como verificar

- **Repositório:** https://github.com/HugoLoyalConsulting/argon-bras-lp
- **Commits e arquivos:** aba `Code` do repositório.
- **Deploys:** aba `Actions` do repositório.
- **Página pública atual:** https://hugoloyalconsulting.github.io/argon-bras-lp/
- **Evidências e handoffs:** diretórios deste repositório, conforme abaixo.

## Estado por onda

| Onda | Estado | Artefatos/evidência | Próximo gate |
|---|---|---|---|
| W0 — Freeze & inventory | IN_PROGRESS | PRD registrada; inventário anterior existe e será migrado para `06-content/assets/` | HG-02 curadoria de assets |
| W1 — Research & validation | IN_PROGRESS | agentes em execução; resultados entrarão em `01-research/` e `02-validation/` | HG-01 fatos/claims |
| W2 — Architecture | IN_PROGRESS | agente em execução; resultados entrarão em `03-architecture/` | HG-01/HG-04 |
| W3 — UX | WAITING_DEPENDENCY | depende da arquitetura | HG-03 |
| W4 — UI / Content | IN_PROGRESS | `design/DESIGN.md` criado pelo agente; demais artefatos aguardam handoff | HG-03 |
| W5 — Build | BLOCKED | não iniciado: depende do gate de design | — |
| W6–W10 — QA, segurança, release, growth | BLOCKED | não iniciados: dependem de build e gates | HG-05 |

## Regras de leitura

- `IN_PROGRESS` significa que há agente com tarefa e artefato/handoff esperado.
- `WAITING_DEPENDENCY` significa que não se deve iniciar antes da dependência.
- `BLOCKED` não significa falha: significa que a PRD exige um gate humano ou um artefato anterior.
- Nenhuma publicação da reconstrução é autorizada por este arquivo. A página pública atual é apenas o baseline separado já existente.
