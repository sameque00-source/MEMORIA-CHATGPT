# CONTINUIDADE MASTER — Open Chat App / Finalização App
Data da atualização: 2026-10-11

## Objetivo desta continuidade
Retomar o OpenChatCut após a formatação do PC sem reiniciar o projeto do zero. Ler a memória persistente, conferir o GitHub real e reconstruir o ambiente necessário. O nome desejado para o novo chat é **Open Chat App — Finalização App**.

## Repositórios oficiais desta tarefa
- Memória de continuidade (público; é o único repositório que foi alterado nesta atualização): https://github.com/sameque00-source/MEMORIA-CHATGPT
- Projeto principal (privado; consultado em modo de leitura nesta atualização): https://github.com/sameque00-source/OpenChatCut
- Backup global do Claude Code (privado; criado antes da formatação): https://github.com/sameque00-source/claude-code-global-backup
- Repositório upstream original do OpenChatCut: https://github.com/0xsline/OpenChatCut
- Documento de plano anterior à formatação, no projeto: https://github.com/sameque00-source/OpenChatCut/blob/main/OPENCHATCUT-ESTADO-PLANO-MESTRE-ANTES-DE-FORMATAR.txt

## Fato crítico: o PC já foi formatado
- A conta/perfil atual do Windows mostrado no PowerShell é C:\\Users\\sameq. Não assumir que o caminho antigo C:\\Users\\User continua sendo o perfil local.
- No PowerShell atual, `node --version` e `git --version` falharam com “não é reconhecido”. Tratar Git e Node como ausentes ou fora do PATH até a instalação/verificação real.
- A saída de `winget --version` ainda não foi fornecida. Verificar se o WinGet está disponível.
- Claude/Claude Code e a interface de FreeLLMAPI estavam sendo configurados. O usuário prefere tudo em português e quer máxima execução autônoma, com perguntas só quando houver um bloqueio real.
- Ainda não foi comprovado nesta sessão que o restaurador foi executado no Windows recém-formatado. Não declarar o ambiente restaurado antes de executar e verificar o resultado.

## Ação imediata: restaurar o Claude Code pelo backup privado
O backup já inclui RESTORE-WINDOWS.ps1, VERIFY-RESTORE.ps1, manifesto de hashes, documentação, coleção de Agents/Skills e configurações sanitizadas. Os relatórios do backup registram verificação de integridade sem divergências no material preservado e testes de componentes; isso não substitui o teste da restauração nesta máquina nova.

Ordem prática recomendada:
1. Em PowerShell, verificar `winget --version`.
2. Se o Git estiver ausente, instalar da fonte oficial pelo WinGet: `winget install --id Git.Git -e --source winget`. Depois fechar e abrir um PowerShell novo e confirmar `git --version`.
3. Clonar o backup privado com caminhos longos: `git -c core.longpaths=true clone https://github.com/sameque00-source/claude-code-global-backup.git "$env:USERPROFILE\Documents\claude-code-global-backup"`.
4. Entrar na pasta e executar: `powershell -NoProfile -ExecutionPolicy Bypass -File .\RESTORE-WINDOWS.ps1`.
5. Durante a restauração, digitar a chave do CodeJato somente quando o script pedir a entrada segura/oculta. Não colocar a chave no chat, GitHub, arquivos Markdown, logs ou comandos digitados visivelmente. A chave não foi preservada no backup por segurança.
6. O script padrão reinstala os plugins habilitados no backup; o guia estima 20–60 minutos para a etapa de plugins. Não usar `-AcceptMarketplaceCommands` automaticamente sem revisar/decidir sobre a execução de comandos de plugins. O backup documenta riscos residuais de plugins e de tokens MCP.
7. Ao terminar, abrir um PowerShell normal novo e executar `powershell -NoProfile -ExecutionPolicy Bypass -File .\VERIFY-RESTORE.ps1`. Não rodar o teste de gateway dentro de uma sessão do Claude Desktop, porque ela pode passar variáveis herdadas que geram falso 401.
8. Ler `%USERPROFILE%\.claude-restore\restore-report-*.md`, o log e o relatório de verificação. Diferenciar `INSTALADO`, `CARREGADO`, `FUNCIONAL`, `INTEGRIDADE` e `SEGURANÇA`. Corrigir falhas verdadeiras e revalidar.

Fontes detalhadas: README.md, RESTORE-GUIDE.md, RESTORE-WINDOWS.ps1, VERIFY-RESTORE.ps1, VERSIONS.md, SECURITY-REPORT.md, RESTORE-TEST-REPORT.md, EXCLUDED-FILES.md e docs/AUDIT-FINDINGS.md dentro de claude-code-global-backup.

## CodeJato — estado e limite de comprovação
- O backup contém o helper `codejato_key.py` e as configurações necessárias para o gateway, mas não a chave real.
- Gateway registrado: `https://api.tn1.top` no ambiente Claude Code. Alguns documentos de OpenChatCut registram a base compatível com Anthropic como `https://api.tn1.top/v1`; antes de configurar o app, ler a implementação atual e verificar como ela concatena `/v1/messages` para evitar duplicar ou omitir `/v1`.
- Alias de modelo registrado: `claude-opus-5-5`; havia aliases Sonnet/Haiku/Fable nas configurações antigas. O alias e o `modelUsage` anunciado pelo gateway não provam, por si só, a identidade do modelo remoto.
- O relatório de segurança do backup registra que o plano CodeJato foi restringido aos apps Claude: chamadas HTTP diretas de scripts receberam 403. O teste do gateway deve ser feito primeiro pelo próprio Claude Code, conforme VERIFY-RESTORE.ps1. Não gastar tempo atribuindo esse 403 automaticamente a um bug do OpenChatCut.
- Separar dois testes: (1) Claude Code com gateway/credencial; (2) OpenChatCut com provider personalizado. A funcionalidade de CodeJato fora dos apps permitidos precisa ser comprovada, não presumida.
- Reintroduzir uma chave é uma etapa que exige a participação do usuário. O script está projetado para recebê-la em modo oculto; não tente recuperar a chave de conversas, variáveis antigas ou arquivos públicos.

## FreeLLMAPI: não confundir com o gateway CodeJato
- A pesquisa/instalação de FreeLLMAPI apareceu como tarefa separada no Claude. Ela não é requisito para restaurar o backup do Claude Code nem para reconfigurar CodeJato.
- Não afirmar que FreeLLMAPI elimina os limites oficiais de cinco horas/semana da assinatura Claude. É um roteador/proxy de provedores; fornecedores gratuitos ou chaves configuradas podem ter quotas, rate limits, fila, autenticação e disponibilidade próprias.
- O comando `curl -fsSL https://freellmapi.co/install.sh | bash` baixa e executa um script remoto em ambiente tipo Unix; não colar diretamente em PowerShell. Se o usuário optar por FreeLLMAPI, inspecionar primeiro o script e as fontes oficiais, confirmar o ambiente compatível (por exemplo WSL, se for suportado) e revisar as alterações antes da execução.
- Se o Claude perguntar sobre instalar Node.js LTS via WinGet, confirmar o requisito do projeto: o OpenChatCut exige Node.js 24.x (`engines` de package.json: `>=24 <25`). Verificar a versão real instalada em vez de aceitar “Node existe” como prova suficiente.

## Estado remoto do OpenChatCut que foi verificado
- Repositório privado: sameque00-source/OpenChatCut; branch padrão `main`.
- `main` tinha HEAD confirmado na consulta recente como `6a7683b0c6f1a9f6423ccc84218dcee731c6f32d`, versão 0.2.14, e commit de documentação `f6ed6304c7fffc3503e482d8bb08626316573fcb` que acrescentou o plano pré-formatação.
- A branch `claude/sharp-ride-bwzrzx` tem package.json na versão 0.3.0 e corresponde à linha de trabalho descrita pelo PR #2. O commit/HEAD exato dessa branch deve ser consultado novamente antes do clone; não inferir que o `main` contém tudo.
- A branch `claude/trusting-edison-7rjeej` tinha package.json na versão 0.2.15, e o PR #1 permanecia aberto na consulta efetuada.
- PR #2 estava aberto na última consulta de 2026-10-11 (última atualização GitHub reportada em 2026-10-02) e descrevia trabalho 0.3.0+: edição longa `condense_video`, gateways customizados, OCR embutido, H.265 e estrutura OpenChatCut Studio.
- A descrição do PR #2 reporta como bloqueios históricos: GitHub Actions falhando em 2–5 segundos/possível limite de orçamento ou minutos; secrets `OPENCHATCUT_E2E_LLM_*` ausentes; auto-update bloqueado sem release pública. Revalidar, pois estes itens vieram do texto do PR, não de um workflow recém-executado nesta sessão.
- O estado de pré-formatação documentava ausência de release e de `.exe` na árvore de `main` em 2026-10-09. Reconsultar releases e Actions antes de afirmar o estado atual.
- Não há checkout local do OpenChatCut disponível a partir dos dados atuais desta conversa. Depois de restaurar Git, conferir branches, PRs, commits, tags, Actions e releases antes de escolher o que clonar. Não assumir que mudanças antigas relatadas em `ef17dc5` ainda existem localmente após a formatação; só contar com o que estiver no GitHub ou em backup verificável.

## Próximas tarefas do OpenChatCut, em ordem
1. Instalar/verificar Git e Node.js 24.x; validar npm e Python real (não só o atalho da Microsoft Store).
2. Conferir no GitHub o HEAD da branch correspondente ao PR #2 e comparar com `main`. Não clonar `main` por hábito.
3. Clonar em uma pasta nova usando o perfil atual. Confirmar HEAD, `git status`, remotes e versão de package.json antes de qualquer alteração.
4. Instalar dependências de forma reproduzível (`npm ci`) e executar lint, testes e build; registrar resultados reais.
5. Reconfigurar/testar CodeJato primeiro no Claude Code com a chave digitada com segurança; não imprimir nem copiar a chave em relatórios.
6. Resolver no app real a configuração do provider LLM. O estado pré-formatação relatava que gateway/harness podiam responder 200 mas o dev server do app apresentava 401 por resolução/slot de provider. Com PC e perfil novos, revalidar do zero antes de chamar de bug confirmado.
7. Testar o fluxo real completo do OpenChatCut: iniciar chat, gerar proposta, aplicar edição na timeline, confirmar persistência/reload, cancelamento e exportação real; inspecionar visualmente e ouvir o vídeo exportado.
8. Criar checkpoint/commit seguro depois de verificar a branch e os testes. Não usar force push, reset destrutivo ou limpeza em massa.
9. Só depois de estabilizar a base, continuar redesign, browser/Playwright/MCP, provider multimodal unificado e roteamento AUTO.

## Regras que o novo chat deve respeitar
- Responder em português brasileiro, de forma direta e sem repetir.
- Maximizar autonomia: fazer inventário, diagnóstico, instalação e verificações sem perguntas intermediárias desnecessárias. Perguntar somente diante de autorização/autenticação, chave que o usuário precisa inserir, comando de marketplace sensível ou bloqueio real.
- Não dizer que executou comandos no computador do usuário se só leu GitHub/documentação. Distinguir fato observado, histórico registrado, hipótese e teste atual.
- MEMORIA-CHATGPT é público: nunca gravar API keys, tokens, cookies, senhas, credenciais, dados privados de sessão ou arquivos locais sensíveis.
- Nesta atualização, apenas o repositório MEMORIA-CHATGPT foi alterado. O repositório OpenChatCut e o backup global foram consultados em leitura; seus arquivos não foram modificados.
- Atualizar esta memória somente com fatos verificados e resultados reais, com data/commit.