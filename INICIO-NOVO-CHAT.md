# INÍCIO DE NOVO CHAT — RECUPERAÇÃO DO OPENCHATCUT

## Atualização pós-formatação — 2026-10-11

Leia primeiro `CONTINUIDADE/OPEN-CHAT-APP-FINALIZACAO-2026-10-11.md`. O PC já foi formatado; o perfil informado é `C:\\Users\\sameq`. O primeiro teste de PowerShell não reconheceu `git` nem `node`; relatório posterior informa Node.js LTS v24.20.0 instalado via WinGet, mas o estado atual de Node/npm/Git ainda deve ser verificado em um terminal novo. O relatório de FreeLLMAPI descreve uma instalação local testada em `D:\\Projetos Claude\\Provedores gratis\\freellmapi`. O backup privado do Claude Code está em `sameque00-source/claude-code-global-backup`. A ordem permanece: verificar ferramentas, restaurar Claude Code, inserir a chave CodeJato somente no prompt seguro, validar com os relatórios reais e depois conferir o estado remoto do OpenChatCut. A chave real não está no backup nem nesta memória.

O prompt completo para o novo chat está em `PROMPTS/PROMPT-INICIAL-OPEN-CHAT-APP-FINALIZACAO.md`. A memória é pública: nunca guardar segredos.

## Como usar
Quando um novo chat começar e o assunto for OpenChatCut, o usuário pode enviar:

> **CONTINUE O OPENCHATCUT. LEIA PRIMEIRO A MEMÓRIA NO GITHUB (sameque00-source/MEMORIA-CHATGPT), RECUPERE TODO O ESTADO ATUAL E CONTINUE EXATAMENTE DE ONDE PARAMOS. NÃO RECOMECE DO ZERO E NÃO PERGUNTE O QUE ESTAMOS FAZENDO.**

## Obrigação do novo chat
Antes de propor ações, reconstruir o contexto pela seguinte ordem:

1. `INICIO-NOVO-CHAT.md`
2. `CONTINUIDADE/OPEN-CHAT-APP-FINALIZACAO-2026-10-11.md`
3. `ESTADO-ATUAL-OPENCHATCUT.md`
4. `PROJETOS/FREELLMAPI-ESTADO.md` — estado, testes reportados, limites e riscos do FreeLLMAPI.
5. `PROJETOS/OPENCHATCUT.md`
6. `DECISOES/OPENCHATCUT.md`
7. `PLANOS/OPENCHATCUT-NEXT.md`
8. `PROVEDORES-E-IA.md`
9. `HISTORICO/OPENCHATCUT-RECENTE.md`
10. `REFERENCIAS-DESIGN/OPENCHATCUT-IMAGENS.md`
11. `PREFERENCIAS.md`
12. Do repositório privado `sameque00-source/claude-code-global-backup`, leia `README.md`, `RESTORE-GUIDE.md`, `RESTORE-WINDOWS.ps1`, `VERIFY-RESTORE.ps1`, `VERSIONS.md`, `SECURITY-REPORT.md` e `RESTORE-TEST-REPORT.md`.
13. Inspecione o estado real do `sameque00-source/OpenChatCut` no GitHub. O checkout local antigo ficava em `C:\\Users\\User\\Downloads\\Aditor de videos IA\\OpenChatCut-ATUAL`, mas não assuma que sobreviveu à formatação; o perfil reportado agora é `C:\\Users\\sameq`.

## Regra principal
A tarefa é continuar o trabalho existente. Não reconstruir o projeto do zero, não trocar arquitetura sem motivo e não apagar mudanças existentes.

## Prioridade
- Primeiro: estado real do checkout/repositório.
- Segundo: testes e evidências.
- Terceiro: memória.
- Quarto: hipóteses.

## Não fazer automaticamente
- Não criar prompts sem o usuário pedir.
- Não fazer varreduras pesadas de agentes/skills quando uma ação direta resolve.
- Não colocar segredos no GitHub.
- Não fazer operações destrutivas.
