# Frontend Parity & PR — atualização incremental

Golden Reference confirmado: **Prime 1.33.1, `main@0d05ae1c`**. A V2 deixou a combinação parcial da base `52ae6567` e recebeu as telas/componentes atuais, preservando a identidade Framixor e os contratos nativos. Versão própria: `2.0.0-falcon9`.

PRs abertos contra `main`: [frontend #7](https://github.com/framixor/prime-house-framixor/pull/7), [backend #42](https://github.com/framixor/framixor-supabase/pull/42). [Checkpoint #6](https://github.com/framixor/engineering-handoffs/pull/6). Commits Framixor preservados; sem merge/deploy.

**READY para revisão de código; CONDITIONAL para homologação STAGING independente; NOT READY para cutover Marley.** [Comparação visual/funcional, evidências e diferenças restantes](FRONTEND_PARITY.md).

Nesta etapa: build Node/typecheck PASS; 206 testes unitários; 9 guardas de endpoints; lint de 310 arquivos alterados sem erros (77 warnings); 8 cenários adicionais de browser PASS, 21 capturas desktop/mobile e 28 rotas sem erros de API. Os fluxos compilados HIC, invoice, pagamento, PDF público e recuperação por UI também foram exercitados. As 28 rotas, isoladamente, não provam paridade visual.

Correções reproduzidas: navegação/telas antigas; alerta indevido após Create & Continue; campos ausentes de detalhes ricos, desconto opcional e itemização; FKs nativas de compras; prefixos de Storage e leitura de branding; contraste e espaço do banner. Caminhos V1 de administração/empresa/invoice foram removidos e Apollo é recusado. Stream local agora tem **68 migrations**, próximo Prime/Flooring **4561**; Platform **4007** permanece reservado.

A importação conciliada anterior e suas auditorias foram preservadas; não houve novo backup, importação, reset ou reauditoria ampla. P2 local explícito: três alertas de monitoramento de backup/scheduler ainda indisponíveis, com preferências desabilitadas. Configuração externa, Auth real, binários históricos, fonte atualizada para cutover e UAT continuam pendentes. Nenhum gap comprovado exige bridge Lovable.

Operações GitHub nesta etapa são autorizadas apenas nos repositórios Framixor; continuam proibidos merge automático, deploy e operações de runtime/dados remotos. Os resultados abaixo descrevem a fase anterior e conservam seus limites e contagens.

---

# Falcon 9 — Flooring V2: checkpoint consolidado

18/10/2026. **CONDITIONAL para homologação controlada em STAGING Framixor; NOT READY para cutover integral de Marley.** A implementação local dos fluxos prioritários e sua auditoria foram executadas. As pendências abaixo separam dados externos ausentes, configuração/homologação e recortes ainda não testados. Nenhuma operação remota foi realizada.

Este é o checkpoint incremental único. Substitui o estado anterior deste mesmo diretório; o Runtime Gap Assessment original (`engineering-handoffs/FALCON9_RUNTIME_GAP_ASSESSMENT_2026-10-18/README.md`, disponível no workspace) permanece imutável. Prime `0d05ae1c` / aplicação 1.33.1 é referência de **código local**, sem afirmação sobre o que foi publicado no PROD.

## 1. Environment & Isolation Evidence

| Componente | Referência |
|---|---|
| Frontend existente | `worktrees/falcon9-parity-frontend`; branch `codex/falcon9-parity-local-20261018`; base `52ae656703c6d831c3d42794a67dd8af655429c9`, preservando os 14 overlays anteriores |
| Backend existente | `worktrees/falcon9-parity-backend/v2`; mesma branch; base `a1addb0921c5d43d8b2ae5c6387f5302be8fda75` mais a V2 local e seus candidatos |
| Golden Reference | `research/prime-house-prod-current@0d05ae1c`, somente leitura |
| Runtime final | PostgreSQL 17, CLI cacheada, Node 24.19.0, Chromium/Playwright; versões/imagens em [environment-isolation.json](evidence/environment-isolation.json) |
| Frontend/browser | `https://falcon9.localhost:8443`; única porta publicada: `127.0.0.1:8443` |
| Auth, REST, Storage | Proxy de mesma origem; gateway interno `supabase_kong_falcon9-parity-20261018:8000` |
| Database | `supabase_db_falcon9-parity-20261018:5432/postgres`, sem publicação no host |

Sete containers próprios, todos em rede Docker `Internal=true`, sem rota default e sem Docker socket no runner. Bootstrap stock vazio antecedeu a contenção; migrations, dados, aplicação e browser só foram executados depois dela. A stack final recebeu **65 migrations via CLI/ledger**, como `postgres` não superuser. Platform `4007` permanece reservado; próximo número Prime/Flooring local: `4558`. Nenhum ledger remoto foi consultado.

Configuração por allowlist, sem copiar `.env`, com chaves locais novas, `V2_LOCAL`, backend nativo `falcon9` e schema `public`. Redirects locais. Hostinger/Google/IA simulados; outros fetches bloqueados e browser sem acesso externo. Não houve chamadas ao runtime, Auth, banco ou Storage Marley, deploy, PR, push, migration/import em STAGING, mensagens reais, cobranças ou registro de crons externos. Checkouts originais e módulos de Claude Code não foram alterados.

O artefato compilado testado usa override local **Nitro `node-server`**; permanece executando localmente. O preset padrão Cloudflare compilou em ensaio anterior, mas seu runtime não foi executado. Isso precisa ser resolvido na escolha do hosting STAGING, sem confundir compilação com homologação.

## 2. Backup, importação e reconciliação

Fonte existente: `~/.apollo13/snapshots/prime-prod-260919/extracted/house-money-manager_260919.backup`. Criada em **19/09/2026 17:45:27 UTC**, 2.429.934 bytes, custom 1.16/zstd, PG 17.6/pg_dump 18.6. SHA-256 `c1b2b489ffd0c8c580b67e6156c61b969dc944ae3479c8394808a557164579b2`, CRC do ZIP verificado, TOC com 2.367 entradas. Cobertura: public 102, Auth 27 e Storage 8 entradas TABLE DATA. Não foi solicitado nem realizado novo backup PROD.

Reutilizados `extract-donor-snapshot.sh`, `bootstrap-prime.mjs`, `import-prime-snapshot.mjs` e `reconcile-prime.mjs`. A extração adicional veio do **mesmo dump**, em PostgreSQL sem rede. SQL, linhas e valores reais continuam privados, fora dos repositórios. Trata-se de **importação transformada para um tenant**, não restore integral do Prime.

Resultado da última stack vazia, confirmado novamente após QA em tenants separados:

- **5.446 registros em 94 tabelas**, incluindo **3.622 eventos de auditoria**. A tabela adicional `knowledge_articles` existe e está vazia na origem.
- **317 campos numéricos compartilhados**, comparação por registro e somatórios financeiros independentes: zero diferenças, sem publicar valores.
- Zero divergências de contagem não explicadas, duplicações, mapeamentos para tenant estrangeiro ou vínculos ativos com tombstones históricos. FKs compostas validadas.
- Uma `proposal_media_usage` já órfã na origem foi excluída. Histórico: 300 eventos de registros apagados receberam 103 identidades históricas estáveis; 231 eventos de entidades globais excluídas permanecem identificados como tal. Zero referências nativas sem mapeamento explicado.
- Repetição do mesmo snapshot/adaptador: **sem escrita**, reconciliação PASS. Destino ocupado ou SHA alterado exige nova stack descartável; não há force merge nem sincronização incremental após cutover.

Cobertura inclui 34 Estimates, 16 Projects, 1 HIC, 2 Change Orders, 18 invoices, 12 recebimentos, 95 compras, 116 despesas, 116 pagamentos de despesas, 96 pagamentos a fornecedores, 55 transações bancárias e 19 aportes. [Reconciliação completa](evidence/import-reconciliation.json).

**Lacunas externas:** 2 usuários/2 identities originais não foram restaurados; 2 atores históricos foram remapeados para identidades sintéticas bloqueadas. Credenciais, sessões e tokens originais não foram importados. Storage contém metadados de 19 objetos/13 buckets, **sem binários**; cinco anexos e duas mídias não recuperam seus arquivos. Documentos assinados originais precisam de preservação própria. Links antigos são revogados, sem fallback Marley. O menor adaptador relacional já está implementado; faltam os insumos de identidade/binários e uma fonte atualizada para cutover.

## 3. Implementação e Prime × V2 Gap Matrix

**PASS refere-se exclusivamente ao recorte exercitado.** A coluna de limites evita equiparar navegação, código ou testes unitários a paridade funcional completa.

| Área | Status / evidência de runtime | Diferença ou limite restante | Prioridade |
|---|---|---|---|
| CRM / Properties / Catalog | **PASS:** Client criado/editado por formulários; Property/Catalog criados/editados pela API, código de catálogo alocado e registros exibidos nas telas compiladas | Variantes completas dos formulários e desativação/exclusão: **NOT TESTED** | P1 UAT |
| Estimates, revisão, cálculo, aceite e conversão | **PASS:** 98 checks API em cada ordem de assinatura; revisão/lineage, custos/anexos, aceite, snapshot, replay e conversão idempotente | Todos os passos dos diálogos e layouts: **NOT TESTED** | P1 UAT |
| Opção de US$1.500 | **PASS:** seleção/aceite no browser, total persistido, snapshot e payload de impressão iguais a US$1.500 | Bug financeiro do checkpoint corrigido em `4511` | P0 resolvido |
| Scope / Share / Sent / Viewed | **PASS:** editor rico grava; IA própria gera/melhora; e-mail simulado grava Sent e visita anônima grava Viewed | Entrega real e qualidade do provedor: **NOT TESTED** | P1 externo |
| HIC / assinaturas / cópia executada | **PASS:** UI compilada gera draft, salva cláusulas, atualiza empresa/registro, congela, coleta duas assinaturas e emite uma entrada; cópia anônima gera PDF e não pode assinar | Originais históricos e revisão jurídica/visual final: **BLOCKED / NOT TESTED** | P0 dados; P1 UAT |
| Invoices / payments / documentos públicos | **PASS:** wizard atual, readiness, emissão, recebimento, saldo/overpayment, PDF público e projeção sem custos internos | Todos os tipos de itemização e entrega real: **NOT TESTED** | P1 UAT |
| Jobs / Change Orders | **PASS:** conversão/baseline, adição/dedução, imposto negativo, piso faturado, edição protegida e início após prazo | Todos os controles de agenda e alteração no browser: **NOT TESTED** | P1 UAT |
| Expenses / Purchases / Vendors / Banking | **PASS:** 13 cenários financeiros, pagamentos, alocação, statement/fingerprint e caixa sem duplicação; extrato compilado sem erro de relação | Reconciliação bancária completa e todos os formulários/relatórios: **NOT TESTED** | P1 UAT |
| Capital / Closing / Distribution | **PASS:** aporte fora da receita, resultado mensal, distribuição, pagamentos/reversões/lock; fechamento mensal compilado carrega | Relatórios anuais e variações de regra: **NOT TESTED** | P1 UAT |
| Auth / usuários / permissões | **PASS:** convite por Hostinger simulado, OTP real local, role/perfil, suspensão/reativação e recovery com redirect confiável | Provisionar/revincular usuários reais e configurar entrega independente | P0 cutover |
| RLS / Storage / branding | **PASS:** tenants separados, FK estrangeira, viewer/staff/admin, contexto ambíguo, upload privado/leitura assinada e negação cross-tenant | Binários históricos ausentes; CORS/CSP/domínios hospedados: **NOT TESTED** | P0 dados; P1 hosting |
| Backup / restore / recuperação | **PASS:** ZIP tenant, checksum/manifest, restauração completa, undo, recuperação pontual por histórico e por backup verificado, rollback atômico, lease e recuperação de worker | Auth/infra global não integram o archive tenant; não é restore do PROD Prime | P1 homologar |
| Jobs agendados | **PASS:** seis cenários nas rotas compiladas: credencial, tenant fixo, idempotência UTC, retenção e continuidade | Rotas novamente desabilitadas; scheduler externo não registrado | P1 ativação |
| Navegação / visual | **PASS:** 28/28 rotas compiladas, sem erros de API nos recortes; identidade Flooring by Framixor preservada | Não certifica todos os workflows nem pixel parity; fontes externas bloqueadas, dispositivos/impressores: **NOT TESTED** | P1 UAT |

Evidências essenciais de código: `queries.useSettings` e `CompanyTab` com `4551` corrigem o contrato nativo de empresa; `public_get_invoice_document`/`4550` corrigem o documento público; `hic-contract.functions.ts` e `hic-copy.functions.ts` implementam o ciclo atual sem alterar o contrato assinado. `tenant-team.server.ts`/`4529` e `tenant-backup.server.ts`/`4530–4546` substituem administração e recuperação proprietárias. Finance mantém o port existente, com a fronteira de execução de `4523`. Tudo nos dois worktrees candidatos.

## 4. Auditoria após implementação

[VALIDATION.md](VALIDATION.md) distingue a geração de regressão, com dados importados e testes destrutivos locais, da última geração limpa preservada. A última importação ficou intacta após QA em tenants próprios.

Passaram typecheck, 111 testes unitários, seis guardas de endpoints e lint dos 159 arquivos TS alterados: zero erros, 29 warnings. Esses gates não fundamentam PASS funcional. A auditoria de catálogo do banco passou nos sete gates de RLS/FKs/roles/search_path/histórico/schemas privados/crons. O engine não possui LOGIN, SUPERUSER ou BYPASSRLS; authenticated não pode assumir seu papel. JWT adulterado, escalada, alterações diretas de histórico, autoatestação de backup, overwrite/delete de arquivo verificado e tentativa cross-tenant foram recusados.

`service_role` fica no servidor para operações Auth delimitadas e atestação fixa de archive, após autoridade tenant/admin verificada; leituras e Storage do backup usam o cliente com RLS. Zero ocorrências da chave privilegiada local nos assets compilados. Publicação de documentos usa tokens aleatórios com hash, expiração/revogação e allowlists. Restore revoga capacidades públicas; não reativa links antigos. Nenhuma URL HTTP absoluta foi encontrada nas colunas textuais de URL/path nem nas 33 colunas JSON auditadas do tenant importado.

Achados resolvidos incluem configuração de empresa incompleta, relação de extrato, lineage de invoice público, auditoria de Sent, segurança de backups, perdas de precisão JSON/UTF-8, ordem de FKs no restore e o uso indevido de tombstones em mídia ativa. [Registro da última correção de importação](evidence/import-validation-findings.json).

Transparência: um ensaio de bootstrap encontrou migrations no diretório temporário e falhou antes de carregar dados reais; o preflight passou a exigir diretório vazio e o replay completo final passou. Houve exposição intermediária de credenciais **descartáveis locais**, seguida de eliminação da stack/volumes e troca de material; nenhuma credencial Marley/backup foi exposta. Falhas de cache/prebundle em desenvolvimento foram registradas; a cópia de cache foi removida e a versão compilada passou inclusive com `/clients` e `/clients/`. O runtime Cloudflare continua **NOT TESTED**.

## 5. Lovable Dependencies

**Nenhum bloqueio funcional comprovado exige Lovable Bridge.** Banco, Auth, Storage, engine financeiro, documentos, equipe e recuperação operam no Supabase independente. Hostinger usa adaptador direto com mailbox por tenant; Places, Address Validation e Static Maps usam APIs próprias; IA usa provedor próprio configurável para Scope/Overview/invoice. Código e runtime simulado: **PASS**. Credenciais/configuração reais, entrega, billing, qualidade e latência: **NOT TESTED**.

Permanece a dependência de build `@lovable.dev/vite-tanstack-config`, além de hooks opcionais de preview e um conector legado opt-in desabilitado. Não foi usado runtime proprietário nem bridge. Manter `LOVABLE_API_KEY` e o opt-in do conector ausentes na configuração independente. Substituir o preset é dívida de build P2, sem justificativa para reintroduzir dependência operacional Marley.

## 6. Top Blockers e Recommended Execution Order

Não há FAIL aberto nos cenários finais executados. Há gates externos para ativação e recortes de UAT explicitamente pendentes; isso impede declarar substituição integral.

1. **P0/S — revisar candidatos e autorizar destino STAGING independente.** Confirmar ownership/ledger sob autorização; escolher hosting Node ou validar Cloudflare. Não aplicar este stream sobre ambientes V1/Apollo compartilhados.
2. **P0/M — preparar Auth, Database e Storage STAGING próprios.** Após autorização específica, aplicar as 65 migrations e provisionar/revincular usuários com papéis corretos. Nenhuma credencial original deve ser restaurada.
3. **P0/M — concluir o pacote de migração de dados.** Para homologação histórica, a fonte local já serve. Para cutover, será necessária uma fonte consistente atualizada, binários, manifest de caminhos e documentos assinados originais; importar e conciliar novamente. Nenhum novo export foi solicitado nesta etapa.
4. **P1/S–M — configurar e validar integrações independentes.** Origins/redirects, segredos server-only, Google próprio e Hostinger por tenant; IA própria. Validar em sandbox/mocks e somente executar chamadas remotas/entregas dentro da autorização concedida. Scheduler permanece desligado até validação.
5. **P1/M — UAT de operação completa.** Variantes de Estimates/revisões, documentos, Banking/Finance, permissões, branding/binários, mobile/print e recuperação no hosting escolhido. Aprovar rollback e reconciliação antes de qualquer decisão de cutover.

**Resumo executivo:** V2 local implementada e exercitada com dados Prime importados e conciliados, backend independente e evidências de isolamento. **CONDITIONAL para solicitar homologação STAGING.** Marley ainda não deve abandonar o Prime: faltam atualização/completude dos dados, identidades/arquivos, configuração externa e aceite operacional dos recortes indicados.
