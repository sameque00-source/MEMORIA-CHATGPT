# Inventário de repositórios GitHub acessíveis

Data da consulta: 2026-10-11  
Conta consultada: `sameque00-source`

## Escopo e limites desta auditoria

Foram listados os repositórios acessíveis pela conta, conferidos os metadados principais (visibilidade, branch padrão, tamanho reportado pelo GitHub), explorados os arquivos da raiz e lidos os READMEs disponíveis para formar um inventário de navegação.

**Isto não é uma auditoria linha a linha de todo o código em todos os projetos.** A análise técnica mais profunda desta continuidade foi focada em:
- OpenChatCut: branches, commits, PRs, workflow runs, releases, `package.json`, plano pré-formatação e prioridades pós-formatação;
- MEMORIA-CHATGPT: arquivos de contexto, continuidade, plano, preferências e prompt do novo chat;
- claude-code-global-backup: guia/automação de restauração, versões, inventário, relatório de segurança e relatório de testes.

Os demais projetos foram catalogados em nível de repositório/raiz e documentação disponível. Não foram alterados nesta missão.

## Inventário atual

Os tamanhos abaixo são a métrica `size` da API do GitHub (aproximadamente em KB de armazenamento Git, não o tamanho exato de download).

| Repositório | Visibilidade / branch | Tamanho reportado | Descrição / observações |
|---|---|---:|---|
| [ZapFlow](https://github.com/sameque00-source/ZapFlow) | Público / `main` | 94 KB | Repositório de app; raiz contém configuração Replit, `package.json`, workspace pnpm e arquivos TypeScript. README é mínimo (`# ZapFlow`). Sem auditoria profunda nesta continuidade. |
| [investigacao-digital](https://github.com/sameque00-source/investigacao-digital) | Privado / `main` | 224 KB | Plataforma de investigação digital autorizada; README descreve auditabilidade, preservação de evidências e cadeia de custódia. Contém `.env.example`, apps, clients, packages, infra e docs. |
| [CLAUDE-MESTRE-FINAL-SKILLS-EM-LOTES-COMPLETO](https://github.com/sameque00-source/CLAUDE-MESTRE-FINAL-SKILLS-EM-LOTES-COMPLETO) | Público / `master` | 34.621 KB | Coleção/arquivo de Agents e Skills, incluindo originais preservados, ZIPs e diretórios `AI-ORCHESTRATOR`, `CLAUDE-CODE-VS-AUTO-ULTIMATE`, `IA-CLOUD-CODE-FINAL-COMPLETO`, `SOURCE-ORIGINAL` e `V2`. Não foi encontrado README.md na raiz. Não reorganizar nem excluir conteúdo sem inventário específico. |
| [OpenChatCut](https://github.com/sameque00-source/OpenChatCut) | Privado / `main` | 92.445 KB | Aplicativo principal: editor de vídeo local-first com IA. É o projeto de trabalho desta continuidade. Branches, PRs, package.json, Actions e releases foram examinados separadamente e estão documentados em `ESTADO-ATUAL-OPENCHATCUT.md` e `CONTINUIDADE/OPEN-CHAT-APP-FINALIZACAO-2026-10-11.md`. Nenhum arquivo do app foi alterado aqui. |
| [Minha-ia](https://github.com/sameque00-source/Minha-ia) | Público / `claude/elegant-lovelace-slefxv` | 230 KB | Projeto de IA; contém `.claude`, `CLAUDE.md`, scripts, docs, source, tests e UI. Não havia README.md na raiz na consulta. Nenhuma mudança feita. |
| [Site-Hamburgueria](https://github.com/sameque00-source/Site-Hamburgueria) | Público / `main` | 52.277 KB | Site Next.js com app, componentes, assets de origem, dados, scripts, public e types. Nenhuma mudança feita. |
| [Imperiom-Fivem](https://github.com/sameque00-source/Imperiom-Fivem) | Privado / `main` | 34.793 KB | Cópia operacional de base FiveM/vRP e arquivos de infraestrutura. README informa que assets de stream GTA de aproximadamente 9,4 GB não estão neste repositório. Nenhuma mudança feita. |
| [antes-da-atualizacao](https://github.com/sameque00-source/antes-da-atualizacao) | Privado / `main` | 131.184 KB | Snapshot/cópia relacionada ao OpenChatCut, com package, source, server, desktop, scripts e arquivos temporários de diagnóstico. A raiz contém diretórios `.cc-check-*`, `.tmp` e `.env.local` reportado com 1 byte. Preservar como snapshot; não limpar nem assumir que seja a base atual sem comparação. |
| [Agentes-de-anuncio-videos-anuncio](https://github.com/sameque00-source/Agentes-de-anuncio-videos-anuncio) | Público / `main` | 0 KB | Repositório vazio segundo a API de conteúdo do GitHub. |
| [hyperframes-video-engine](https://github.com/sameque00-source/hyperframes-video-engine) | Privado / `main` | 11.120 KB | Projeto de vídeo baseado no HyperFrames (HTML/CSS/JS + animação GSAP renderizada em MP4), com `.agents`, docs, manifesto e lock de Skills. Nenhuma mudança feita. |
| [MEMORIA-CHATGPT](https://github.com/sameque00-source/MEMORIA-CHATGPT) | Público / `main` | 80 KB | Memória persistente de contexto e continuidade. **É o único repositório alterado nesta missão.** Por ser público, não pode conter chaves, tokens, senhas, cookies ou credenciais. |
| [claude-code-global-backup](https://github.com/sameque00-source/claude-code-global-backup) | Privado / `main` | 73.221 KB | Backup do Claude Code criado antes da formatação, com manifesto, scripts PowerShell de restauração/verificação, relatórios de segurança/testes e coleção de configuração. Foi somente lido; não foi alterado nesta missão. |

## Regras de continuidade

1. Não confundir `OpenChatCut` com `antes-da-atualizacao`: são repositórios distintos. Inspecionar histórico e estado remoto antes de escolher uma base.
2. Não misturar esta tarefa com projetos como ZapFlow, FiveM, Site-Hamburgueria, HyperFrames ou investigacao-digital.
3. A única alteração autorizada nesta missão é a memória persistente em `MEMORIA-CHATGPT`.
4. Antes de alterar qualquer projeto, conferir branch, HEAD, estado, PRs, releases, arquivos locais não versionados e segredos.
5. Não considerar os repositórios “auditados por completo” apenas porque foram listados. Os projetos fora do escopo aprofundado precisam de auditoria específica caso o usuário queira trabalhar neles.
6. Não colocar segredos nem dados privados de sessão na memória pública.

## Próximo foco desta continuidade

O foco atual é **Open Chat App — Finalização App**, isto é, continuar o OpenChatCut após a formatação. Ordem de trabalho:
1. verificar `winget`, Git, Node 24.x e npm no PowerShell atual;
2. restaurar o ambiente Claude Code pelo backup privado e executar `VERIFY-RESTORE.ps1`;
3. recolocar a chave CodeJato somente via entrada oculta do restaurador e validar pelo próprio Claude Code;
4. decidir branch/commit do OpenChatCut com base nos remotos atuais;
5. validar provider LLM dentro do app e o fluxo de edição real até exportação;
6. depois tratar redesign e integrações futuras.

FreeLLMAPI tem seu próprio documento em `PROJETOS/FREELLMAPI-ESTADO.md`. De acordo com o relatório fornecido pelo usuário, ele está instalado em `D:\Projetos Claude\Provedores gratis\freellmapi`, mas isso não comprova eliminação dos limites oficiais do Claude e não substitui a restauração do CodeJato.
