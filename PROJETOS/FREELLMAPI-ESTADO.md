# FreeLLMAPI — estado operacional pós-formatação

Data do relatório: 2026-10-11  
Origem deste registro: relatório enviado pelo usuário. Os testes abaixo são fatos **relatados**; não foram reexecutados independentemente pelo ChatGPT nesta atualização.

## Identificação

- Projeto: `tashfeenahmed/freellmapi`
- Diretório local: `D:\Projetos Claude\Provedores gratis\freellmapi`
- Tipo: gateway/roteador local para APIs de modelos de linguagem, compatível com endpoints OpenAI e Anthropic.
- Endpoint local reportado: `http://127.0.0.1:3001`
- Acesso: ligado ao loopback (`127.0.0.1`), sem intenção de exposição à rede local.
- O comando divulgado `curl -fsSL https://freellmapi.co/install.sh | bash` é um padrão de shell tipo Unix. Não deve ser colado diretamente no PowerShell. O relatório indica que a cópia local já foi instalada a partir do repositório GitHub, portanto não reinstalar sem motivo.

## Ambiente e instalação reportados

- Node.js LTS v24.20.0 instalado por WinGet a partir da fonte oficial.
- Dependências npm instaladas por `npm install`: 834 pacotes.
- `npm audit` relatou vulnerabilidades em dependências de terceiros. Não foi executado `npm audit fix --force`, pois pode introduzir alterações incompatíveis.
- O estado atual do comando `git --version` não foi informado após a formatação. A primeira tentativa registrada no PowerShell não reconheceu `git` nem `node`; o relatório posterior informa instalação de Node, mas a validação atual ainda deve ser repetida num PowerShell novo.

## Arquivos e configuração locais — não publicar

- `.env`: contém uma chave de encriptação própria, além das configurações de porta/acesso. Manter só local; nunca enviar à memória pública ou a um repositório sem sanitização.
- `.admin-credentials.json`: relatório diz que guarda a senha de administrador gerada automaticamente. Está no `.gitignore`; manter privado e não copiar para GitHub, chat, logs ou relatórios.
- `.claude/launch.json`: registra o servidor como preview do Claude Code (`freellmapi-server`, porta 3001).
- `usar-no-claude-code.ps1`: ativa a integração só na janela de terminal em que é executado. É uma opção local e reversível; não é uma mudança global.
- A chave de encriptação, senha do painel e demais segredos reais não devem ser incluídos neste documento ou em qualquer commit.

## Provedores sem cadastro reportados

| Provedor | Catálogo reportado | Observações |
|---|---:|---|
| Kilo Gateway (`kilo`) | 13 modelos | Teste `kilo-auto` retornou HTTP 200 via AtlasCloud através do Kilo. |
| OVHcloud AI Endpoints (`ovh`) | 14 modelos | Quota reportada de aproximadamente 2 requisições/minuto por IP e por modelo. |
| AI Horde (`aihorde`) | 16 modelos | Usa chave anônima padrão da comunidade; disponibilidade/fila pode variar. |

Provedores que exigem conta ou chave própria (incluindo Groq, OpenRouter, Mistral, Cohere, NVIDIA, Cloudflare, Google e Hugging Face) não foram configurados, segundo o relatório.

## Testes registrados no relatório

| Verificação | Resultado relatado |
|---|---|
| Servidor em `http://127.0.0.1:3001` | OK |
| `/v1/models` | Catálogo retornado |
| Chamada a `kilo-auto` | HTTP 200, resposta real de provedor de terceiros através do Kilo |
| Roteador `auto` | Resposta via Poolside (`poolside/laguna-s-2.1:free`) |
| Endpoint Anthropic-compatível `/v1/messages` | HTTP 200 com formato de resposta compatível |

Estes testes demonstram o comportamento relatado da instalação e dos provedores naquele momento; não provam disponibilidade futura ou cotas ilimitadas.

## Limites e identidade do modelo

- As cotas de provedores sem cadastro são externas e podem variar. O relatório cita Kilo em torno de 200 requisições/hora por IP e OVH em torno de 2 requisições/minuto por IP/modelo. Esses números são aproximados, não garantias.
- Resposta em HTTP 200 prova que uma chamada respondeu; não comprova que o modelo seja um Claude oficial.
- O relatório diz explicitamente que a resposta real veio de modelos de terceiros (por exemplo AtlasCloud/Kilo e Poolside), e não do modelo oficial Anthropic Opus 5.5, mesmo que alguma integração exponha um alias semelhante a Claude.
- FreeLLMAPI não é uma forma comprovada de remover os limites oficiais semanais ou de cinco horas da assinatura Claude. Ele pode usar provedores e quotas separados, cada um com seus limites, disponibilidade, filas e políticas.
- Não apontar o Claude Code globalmente para FreeLLMAPI. O script dedicado deve ser usado apenas quando o usuário decidir conscientemente executar uma sessão com os provedores gratuitos.

## Próxima sequência recomendada

1. Verificar em novo PowerShell `node --version`, `npm --version`, `git --version` e `winget --version`. Não reinstalar Node se a versão já estiver correta.
2. Restaurar a configuração global do Claude Code a partir do repositório privado `sameque00-source/claude-code-global-backup`, seguindo `RESTORE-GUIDE.md`.
3. Durante `RESTORE-WINDOWS.ps1`, inserir a chave CodeJato apenas no prompt de entrada oculta. A chave real não está no backup nem nesta memória pública.
4. Executar `VERIFY-RESTORE.ps1` em um PowerShell normal novo; guardar e ler os relatórios sanitizados. Não rodar teste do gateway dentro de um processo com variáveis herdadas do Claude Desktop.
5. Testar CodeJato pelo próprio Claude Code. O relatório de segurança do backup informa que chamadas HTTP diretas podem retornar 403 porque o plano é restrito aos apps do Claude.
6. Depois, auditar a branch remota correta do OpenChatCut, restaurar o projeto, validar a configuração de provider real e testar o fluxo completo de edição/exportação.
7. Tratar correção de vulnerabilidades npm como tarefa separada: inspecionar o audit e escolher correções compatíveis; não executar `npm audit fix --force` de modo cego.

## Links

- Repositório fonte: https://github.com/tashfeenahmed/freellmapi
- Backup privado Claude Code: https://github.com/sameque00-source/claude-code-global-backup
- Memória: https://github.com/sameque00-source/MEMORIA-CHATGPT
- Aplicativo: https://github.com/sameque00-source/OpenChatCut
