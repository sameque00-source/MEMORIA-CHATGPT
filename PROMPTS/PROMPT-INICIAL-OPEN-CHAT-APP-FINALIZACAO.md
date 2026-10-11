# PROMPT INICIAL — Open Chat App / Finalização App

Nome desejado para o chat na lateral: **Open Chat App — Finalização App**.

Você está retomando um trabalho existente após a formatação do PC. Não comece do zero e não invente estado. Sua primeira missão é ler a memória no GitHub, verificar o código real e restaurar o ambiente a partir do backup. Trabalhe em português brasileiro, com máxima autonomia e de forma objetiva.

## REGRAS OBRIGATÓRIAS
1. Execute o trabalho até o fim sem pedir confirmações para etapas comuns. Só interrompa diante de um bloqueio real, autenticação ou segredo que eu precise fornecer, ou uma ação de segurança que exija decisão humana.
2. Leia todos os documentos listados abaixo antes de decidir os próximos passos. Não se baseie só neste prompt.
3. Verifique o estado real do GitHub. Separe fatos observados de informações históricas e hipóteses. Não afirme ter acessado o computador ou executado comandos se isso não ocorreu.
4. Nesta tarefa de preparação, altere apenas a memória no repositório MEMORIA-CHATGPT quando precisar documentar estado. Não faça commits, pushes, alterações ou limpezas no repositório OpenChatCut até ter auditado o remoto e explicado/validado qual branch e commit contêm o trabalho correto.
5. Nunca coloque API keys, tokens, senhas, cookies ou credenciais em GitHub, relatórios, arquivos Markdown ou mensagens. A memória MEMORIA-CHATGPT é pública.
6. Preserve histórico Git e arquivos. Não use force push, reset destrutivo, git clean -fd nem exclusões em massa.
7. Use o menor conjunto de ferramentas que resolva a tarefa; agentes/skills em paralelo somente quando forem úteis. Se houver limite, diminua a concorrência e continue.
8. Não confunda nome de modelo/alias com prova da identidade real do modelo remoto.

## FONTES QUE VOCÊ DEVE LER
Memória persistente pública: https://github.com/sameque00-source/MEMORIA-CHATGPT
Leia integralmente, nesta ordem:
- README.md
- INICIO-NOVO-CHAT.md
- CONTINUIDADE/OPEN-CHAT-APP-FINALIZACAO-2026-10-11.md
- ESTADO-ATUAL-OPENCHATCUT.md
- PROJETOS/FREELLMAPI-ESTADO.md
- PROJETOS/OPENCHATCUT.md
- DECISOES/OPENCHATCUT.md
- PLANOS/OPENCHATCUT-NEXT.md
- PROVEDORES-E-IA.md
- HISTORICO/OPENCHATCUT-RECENTE.md
- REFERENCIAS-DESIGN/OPENCHATCUT-IMAGENS.md
- PREFERENCIAS.md

Projeto OpenChatCut (privado; primeiro só leitura para determinar o estado correto): https://github.com/sameque00-source/OpenChatCut
Leia também, integralmente, o documento mestre pré-formatação:
https://github.com/sameque00-source/OpenChatCut/blob/main/OPENCHATCUT-ESTADO-PLANO-MESTRE-ANTES-DE-FORMATAR.txt
Inspecione README.md, package.json, .gitignore, scripts de teste, workflows CI/desktop, branches, commits, tags, PRs e releases. Compare main com a branch/PR mais avançada antes de clonar ou alterar qualquer coisa. Não presuma que main possui toda a implementação.

Backup privado do Claude Code, já criado antes da formatação: https://github.com/sameque00-source/claude-code-global-backup
Leia README.md, RESTORE-GUIDE.md, RESTORE-WINDOWS.ps1, VERIFY-RESTORE.ps1, BACKUP-MANIFEST.json, DEPENDENCIES.md, VERSIONS.md, SECURITY-REPORT.md, RESTORE-TEST-REPORT.md, EXCLUDED-FILES.md e docs/AUDIT-FINDINGS.md. O backup possui os scripts de restauração; não reimplemente esses scripts sem uma falha comprovada.

## SITUAÇÃO ATUAL DO WINDOWS
Já formatei o PC. Meu perfil Windows atual é C:\Users\sameq. O primeiro PowerShell não reconheceu `node` nem `git`; depois, o relatório do FreeLLMAPI informou Node.js LTS v24.20.0 instalado via WinGet e dependências do projeto instaladas. Verifique no terminal novo `winget --version`, `node --version`, `npm --version` e `git --version`. Não presuma que Git esteja instalado, e não reinstale Node sem conferir primeiro.

## PRIMEIRA MISSÃO — RESTAURAR O CLAUDE CODE
1. Verifique se o WinGet está disponível.
2. Se Git não estiver instalado, use a fonte oficial/WinGet: winget install --id Git.Git -e --source winget. Depois abra um PowerShell novo e valide git --version.
3. Clone o backup privado, usando caminho longo:
   git -c core.longpaths=true clone https://github.com/sameque00-source/claude-code-global-backup.git "$env:USERPROFILE\Documents\claude-code-global-backup"
4. No diretório clonado, examine as instruções do README e execute RESTORE-WINDOWS.ps1 de acordo com RESTORE-GUIDE.md. O script está preparado para adaptar caminhos do perfil antigo C:\Users\User ao perfil atual.
5. O script pede a chave CodeJato usando entrada oculta e grava-a localmente com ACL restrita. A chave não está no GitHub por segurança. Quando o prompt seguro do script aparecer, preciso digitar a chave ali; não me peça para colá-la no chat e não tente recuperar a chave de conversas antigas.
6. O script padrão reinstala os plugins habilitados do backup, uma etapa que pode demorar. Não aceite comandos de marketplaces de forma indiscriminada: não use a opção de aceitar automaticamente comandos de plugins sem revisar o risco descrito em SECURITY-REPORT.md.
7. Depois da restauração, em um PowerShell normal novo, execute VERIFY-RESTORE.ps1. Leia os relatórios de restore e verify. Resolva erros reais e repita o teste. Não execute a verificação do gateway dentro do Claude Desktop, pois as variáveis herdadas podem causar um falso 401.
8. Confira que Node e npm existem e que a versão do Node é 24.x, exigida pelo OpenChatCut. Se o Node LTS instalado não estiver no intervalo >=24 <25, corrija com uma fonte oficial antes de instalar dependências do app. Instale/valide Python real se o relatório pedir; não confunda o atalho da Microsoft Store com Python real.

## SEGUNDA MISSÃO — CONFIGURAR E VALIDAR CODEJATO
Configuração histórica: gateway CodeJato em https://api.tn1.top, alias principal claude-opus-5-5, esforço máximo. As chaves reais não foram copiadas no backup.
Use o fluxo seguro provido pelo restaurador e valide o gateway pelo próprio Claude Code, conforme o VERIFY-RESTORE.ps1. Os relatórios registram que chamadas HTTP diretas de scripts podem devolver 403 porque o plano pode estar limitado aos apps Claude. Não confunda esse bloqueio com um bug do OpenChatCut.
Se o setup falhar, investigue primeiro a saída sanitizada, status HTTP e configuração de URL/protocolo sem exibir a chave. Não faça alterações aleatórias entre Bearer, x-api-key, URLs ou sufixos /v1. Inspecione o protocolo exigido e os pontos em que o app concatena /v1/messages.
Depois, configure e teste CodeJato no OpenChatCut como uma tarefa separada; confirme que o plano permite uso fora do Claude Code antes de gastar tempo com chamadas diretas. Um alias não comprova a identidade real do modelo.

## TERCEIRA MISSÃO — RETOMAR OPENCHATCUT
Depois da restauração do ambiente, confira o estado remoto real do projeto e escolha a branch correta com base em HEADs, PRs e package.json atuais. A memória registra main em 0.2.14 e uma linha de desenvolvimento 0.3.0 ligada ao PR #2, mas isso deve ser revalidado; não faça clone automático de main sem comparar.
Próxima prioridade técnica original: revalidar o caminho real de configuração de provider/LLM no servidor do app. Antes da formatação havia um 401 no app real apesar de testes isolados de gateway/harness que responderam 200. Após a formatação, trate esse relato como histórico e reproduza o caso atual antes de afirmar que o bug continua.
Após instalar as dependências com npm ci, executar lint, testes, build e registrar os resultados efetivos. Depois validar uma edição real completa: importar mídia, analisar/transcrever, pedir proposta ao agente, aplicar mudanças à timeline, verificar persistência/reload e cancelamento, exportar o vídeo e inspecionar visualmente/escutar o arquivo final. Só então consolidar mudanças em commit seguro.
Redesign, browser/Playwright/MCP, provider multimodal unificado e AUTO routing são etapas posteriores; não antecipar expansão antes da base funcionar.

## FREELLMAPI — JÁ INSTALADO SEGUNDO O RELATÓRIO, OPCIONAL

Leia `PROJETOS/FREELLMAPI-ESTADO.md`. O relatório do usuário informa que a cópia está em `D:\Projetos Claude\Provedores gratis\freellmapi`, com Node.js LTS v24.20.0, 834 pacotes, serviço em `127.0.0.1:3001`, e testes reportados para Kilo, OVH, AI Horde e compatibilidade Anthropic. Registre os resultados como reportados pelo usuário, salvo se forem novamente testados.

Não execute `curl -fsSL https://freellmapi.co/install.sh | bash` diretamente no PowerShell nem reinstale tudo cegamente. Não envie `.env` nem `.admin-credentials.json` ao GitHub. `npm audit` indicou vulnerabilidades; não usar `npm audit fix --force` sem examinar incompatibilidades.

FreeLLMAPI não comprova remover limites oficiais da assinatura Claude. Os provedores gratuitos têm quotas/filas próprias e a resposta de AtlasCloud/Kilo ou Poolside não é o modelo oficial Anthropic Opus 5.5. O script `usar-no-claude-code.ps1` foi descrito como ativação apenas por terminal; não substituir a configuração global.

Prioridade: restaurar Claude Code pelo backup privado, recolocar a chave CodeJato no prompt oculto do restaurador e executar VERIFY-RESTORE. A chave real nunca deve ser pedida no chat nem colocada em arquivo público.
## PORTUGUÊS E NOME DO CHAT
Responda e documente tudo em português brasileiro. O usuário quer a interface e as instruções do Claude em português sempre que suportado; a configuração anterior de workspace tinha Brazilian Portuguese, mas a tradução de todos os elementos da interface depende da versão/app. Use o título desejado: Open Chat App — Finalização App. Se não for possível mudar o título pela interface/ação disponível, informe apenas que o usuário precisa renomear manualmente na lateral.

## CRITÉRIOS DE CONCLUSÃO
- Repositórios e documentos foram lidos e resumidos com links exatos.
- Backup do Claude Code restaurado com relatório gerado e verificação executada na máquina nova.
- Node/Git/Python necessários instalados e versões verificadas.
- Chave CodeJato digitada apenas no prompt seguro e teste feito via Claude Code, sem exposição.
- Branch e commit corretos do OpenChatCut identificados pelo estado remoto atual.
- Nenhum segredo publicado ou exibido.
- Plano atualizado na memória com o que passou, o que falhou, logs sanitizados, commit/branch/links e próximo passo único.
- Não declarar algo como concluído se foi apenas planejado.

Comece lendo as fontes. Em seguida, retome a restauração do backup e continue automaticamente. Não peça para eu repetir informações que já estão registradas.