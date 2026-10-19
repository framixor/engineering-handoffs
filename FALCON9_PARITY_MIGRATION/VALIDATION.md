# Incremento Frontend Parity & PR

A validação nova está em [FRONTEND_PARITY.md](FRONTEND_PARITY.md). O ledger local recebeu apenas 4558–4560, após falhas reproduzidas do frontend; 68 migrations no total. QA permaneceu em tenants sintéticos separados. Importação, financeiro, RLS e recuperação abaixo são evidências concluídas da fase anterior, sem reiniciar suas auditorias. Os resultados novos não certificam variantes que continuam NOT TESTED.

---

# Falcon 9 — evidências e limites da validação

18/10/2026. Referência: Prime local `0d05ae1c`; candidatos na branch `codex/falcon9-parity-local-20261018`. Os resultados são locais, sem certificação de publicação ou execução em PROD.

## Gerações e integridade da evidência

1. **Regressão de implementação:** stack descartável com dados importados, fixtures sintéticas, engine financeiro, equipe, integrações simuladas e recuperação destrutiva. Após as correções, todos os cenários registrados abaixo passaram. A geração foi eliminada para repetir o importador atualizado.
2. **Replay limpo final:** 65 migrations, banco vazio, importador final com separação de tombstones e dados ativos, 5.446 registros/94 tabelas, 317 colunas numéricas. Repetição imediata sem escrita; repetição após QA em tenants próprios também sem escrita e conciliada. Essa geração foi preservada. O tenant `prime-house-flooring` não recebeu as fixtures financeiras dos testes anteriores.
3. **Artefato compilado final:** Nitro `node-server`, chaves locais da última stack, fontes com hashes iguais ao candidato. Browser novo, sem importar módulos `/src/`; Auth, documentos, backup, CRUD e navegação reais. O preset Cloudflare compilou antes, mas seu runtime não foi testado.

Não são publicados SQL extraído, linhas reais, somatórios financeiros, usuários originais, tokens, credenciais, headers ou logs brutos. Os PDFs e screenshot publicados contêm somente dados sintéticos.

## Gates executados

| Gate | Resultado | Evidência |
|---|---|---|
| Ledger local completo / owner não superuser | **PASS — 65** | [cli-replay.json](evidence/cli-replay.json) |
| Carga final, FKs, contagens, numéricos e histórico | **PASS — 94 tabelas / 5.446 registros / 317 campos** | [import-reconciliation.json](evidence/import-reconciliation.json) |
| Regressão API, cliente assinando primeiro | **PASS — 98/98** | [golden-client-first-results.json](evidence/golden-client-first-results.json) |
| Regressão API, contractor assinando primeiro | **PASS — 98/98** | [golden-contractor-first-results.json](evidence/golden-contractor-first-results.json) |
| Finance, Banking, Capital, Closing, Distribution | **PASS — 13 cenários** | [finance-runtime.json](evidence/finance-runtime.json) |
| FK/RLS/permissões, invoice público, CO, revisão e alertas | **PASS — 9 cenários** | [infra-runtime.json](evidence/infra-runtime.json) |
| Opção US$1.500, aceite e payload de impressão | **PASS** | [runtime-options-results.json](evidence/runtime-options-results.json) |
| CRM, Rich Scope, Scope/Overview/Vendor AI, Google, e-mail, Storage e directory | **PASS — 10 gates; provedores simulados** | [runtime-parity-results.json](evidence/runtime-parity-results.json) |
| Convite, OTP, permissões, suspensão/reativação e recovery | **PASS — 4 gates** | [team-runtime-results.json](evidence/team-runtime-results.json) |
| Backup completo, verificação, restore e undo | **PASS — 2 gates funcionais + login** | [recovery-development-results.json](evidence/recovery-development-results.json) |
| Recovery adversarial | **PASS — 10 gates** | [recovery-adversarial-results.json](evidence/recovery-adversarial-results.json) |
| Wizard invoice, recebimento, PDF público e backup pela UI | **PASS — 4 gates compilados** | [production-invoice-results.json](evidence/production-invoice-results.json) |
| HIC draft/cláusulas/refresh, duas assinaturas, PDF executado | **PASS — 3 gates compilados** | [production-hic-results.json](evidence/production-hic-results.json) |
| Client criado/editado nos formulários compilados | **PASS** | [production-crm-results.json](evidence/production-crm-results.json) |
| Property/Catalog API + leitura UI; fechamento mensal UI | **PASS — 2 recortes compilados** | [production-master-data-results.json](evidence/production-master-data-results.json) |
| Envio da cópia HIC assinada, auditoria e imutabilidade | **PASS — transporte Hostinger simulado** | [signed-copy-mail-results.json](evidence/signed-copy-mail-results.json) |
| Scheduled/continue/retention no artefato compilado | **PASS — 6 gates; desabilitados depois** | [jobs-runtime-results.json](evidence/jobs-runtime-results.json) |
| Navegação compilada | **PASS — 28/28 rotas**, sem certificar todos os workflows | [production-navigation.json](evidence/production-navigation.json) |
| Auditoria SQL de RLS, FKs, roles, helpers, search_path, histórico e crons | **PASS — 7 gates** | [security-final.json](evidence/security-final.json) |
| Chave service_role local no cliente compilado | **PASS — zero ocorrências** | [client-secret-boundary.json](evidence/client-secret-boundary.json) |
| URLs nos campos de assets e JSON importados | **PASS — sem URLs HTTP encontradas** | [assets](evidence/imported-asset-url-audit.json), [33 colunas JSON](evidence/nested-url-audit.json) |
| Typecheck, Vitest, guardas e lint alterado | **PASS — 111 testes / 6 guardas / 159 arquivos lint**, zero erros e 29 warnings | [quality-gates.json](evidence/quality-gates.json) |

Typecheck, testes unitários, lint e build são gates de qualidade; não são usados isoladamente para marcar uma funcionalidade como PASS.

## Recortes da auditoria

Finance: preço/entrada/saldo, revisões, snapshot congelado, conversão única, exatamente uma invoice de entrada, recebimento parcial/final, bloqueio de excesso, compra/alocação, vendor payment sem dupla contagem, aportes fora da receita, caixa, resultado, distribuição, reversão e período bloqueado. Todos os valores dos testes de escrita são sintéticos.

RLS/segurança: tenant estrangeiro e FK estrangeira, viewer sem escrita/delete, staff sem edição de settings, admin restrito ao tenant, contexto ambíguo, JWT adulterado, tentativa de assumir o engine, tabelas sem grant anon, schemas de importação/recovery privados, autoatestação de backup proibida e link executado incapaz de assinar. A ausência de `service_role` no bundle usa o material local exato; nenhum segredo remoto foi carregado.

Recuperação: arquivo tenant real com manifest/checksums e números preservados como texto, Storage privado, preview, substituição completa e undo, recuperação pontual por histórico e por backup verificado, lease que bloqueia somente o tenant afetado, arquivo verificado imutável, retenção do último backup, corrupção/tenant estrangeiro recusados, falha de FK com rollback completo e worker abandonado recuperado. Auth, roles e infraestrutura global não são restaurados pelo archive tenant.

Scheduler: credencial inválida recusada; tenant fixo por configuração server-only; entrada de tenant na requisição ignorada; uma execução por dia UTC; último archive verificado protegido; exclusão somente elegível no próprio tenant; continuidade de ID estrangeiro recusada. Nenhum cron externo foi criado. O controlador retornou a configuração para desabilitada.

## Artefatos visuais sintéticos

- [Invoice público em PDF](evidence/synthetic-public-invoice.pdf)
- [HIC executado em PDF](evidence/synthetic-executed-hic.pdf)
- [CRM compilado com identidade Framixor](evidence/synthetic-production-crm.png)

São provas de renderização, sem comparação pixel a pixel contra uma UI de produção. Fontes externas foram bloqueadas/simuladas no browser.

## Limites e decisões

A origem de setembro não certifica o estado de outubro. Faltam binários, documentos originais e identidades operacionais. Entrega real Hostinger, Google com configuração/billing reais, qualidade/latência da IA, CORS/CSP/origins hospedados, Cloudflare runtime, carga concorrente, dispositivos/impressores e todas as variantes de formulários permanecem NOT TESTED.

Os resultados finais corrigidos substituem falhas de desenvolvimento registradas, sem apagá-las do diagnóstico privado. A inspeção de contagens detectou uma tentativa de usar tombstone histórico como vínculo ativo de mídia; a geração foi descartada, o join foi restringido e a carga final confirmou uma órfã excluída e zero vínculos ativos históricos. Uma falha anterior de bootstrap produziu a guarda de diretório vazio. Material local descartável exposto em uma inspeção anterior foi invalidado pela eliminação da stack e rotação; não houve exposição de credenciais Marley ou do backup.

Reprodução: `worktrees/falcon9-parity-backend/v2/scripts/dev/rehearsal/README.md`. Os scripts fixam a identidade da stack e falham sem recursos locais/isolamento. `rebuild-local.sh` exige `FALCON9_DISPOSABLE=1`, não faz reset implícito e adiciona fixtures; executá-lo apenas em geração descartável. Arquivos temporários privados não devem ser copiados para Git.
