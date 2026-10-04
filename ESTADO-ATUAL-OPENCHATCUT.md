# ESTADO ATUAL — OPENCHATCUT

## Identidade do projeto
OpenChatCut = editor de vídeo local-first com IA, agente conversacional, linha do tempo multitrack real, edição reversível, Remotion para renderização e MCP para agentes externos.

Checkout de trabalho local:
`C:\Users\User\Downloads\Aditor de videos IA\OpenChatCut-ATUAL`

Repositório GitHub principal:
`sameque00-source/OpenChatCut`
Visibilidade: privado.
Branch padrão do GitHub: `main`.

## Estado local conhecido
- Branch de trabalho: `claude/sharp-ride-bwzrzx`
- Último commit-base conhecido: `75d1342` — `feat(agent): editing depth Low/Medium/High/Extra/Ultra; run status shows only real states`
- Após esse ponto havia dezenas de arquivos modificados e alguns arquivos novos ainda sem commit. Não assumir que `main` representa 100% do estado local mais recente.
- Há foco em estabilização e validação antes de fazer grandes ampliações.

## O que já foi corrigido
1. Gateway CodeJato/Headroom: textos longos eram comprimidos em hashes em torno de ~450–600 caracteres. Corrigido com blocos de relay menores (~360 chars) + teste.
2. SSE `data: {}`: causava falhas perto de ~601 s. Filtro/retry corrigidos.
3. Propostas de edição longas eram descartadas como stale após ~18 min porque a transcrição alterava o projeto em background. A checagem de stale passou a ignorar campos de transcrição.
4. Caminho do modelo ASR estava incorreto (`ggml` vs `ggerganov/whisper.cpp`). Corrigido.
5. Speech analysis usava sempre `large-v3-turbo/auto`. Agora respeita modelo/idioma configurados.
6. `remove_silence` retornava `edited: []` sem efeito. Corrigido e testado.
7. `edit_item` de áudio rejeitava campo desconhecido/ausência de faixa de áudio. Corrigido e testado.
8. Cancelamento após restart. Corrigido.
9. Loop de escrita do `.env.local`. Corrigido.
10. Teste `music-media.verify.ts` estava escrevendo no diretório real por causa de `~/.openchatcut/data-dir.json`. Teste passou a usar perfil/data-dir isolado antes do dynamic import.
11. `verify-gate-coverage` marcava `*.verify.*` de backup como teste órfão. Corrigido para excluir `backups/`.
12. Suite de verificação chegou a exit code 0, com ~613 arquivos verify alcançáveis/registrados e sem falhas reais no conjunto; algumas falhas reportadas são intencionais/esperadas.

## Testes e validação
- Foram executadas validações de gateway, harness e suíte de verify.
- O gateway CodeJato respondeu 200 externamente com o modelo oficial `claude-opus-5-5`.
- O harness de E2E pode obter 200 quando recebe diretamente as variáveis `OPENCHATCUT_E2E_LLM_*`.
- O problema que restou na validação real do app era de resolução de configuração/credencial dentro do servidor de desenvolvimento: o harness e o gateway funcionavam, mas o dev server não estava lendo a mesma credencial/configuração. O servidor estava sendo iniciado sem o slot compatível correto e havia entradas `LLM_CUSTOM_1/2/3_*` antigas apontando para localhost. A próxima validação deve eliminar esse 401 no app real, reiniciando o dev server após a configuração correta.

## Configuração de IA conhecida
Gateway CodeJato:
- Base Anthropic compatível: `https://api.tn1.top/v1`
- Modelo usado/testado: `claude-opus-5-5`
- O modelo retornou identificação oficial `claude-opus-5-5` em teste HTTP 200.
- No Claude Desktop, a preferência definida foi: Opus 5.5 + contexto de 1M + esforço Máximo.
- Não armazenar a API key nesta memória.

## Problema imediato / próxima validação obrigatória
Resolver e comprovar o caminho real:
`.env.local / keystore -> provider slot do app -> dev server -> chamada LLM -> proposta -> edição -> estado do projeto`.

Depois disso, rodar novamente o fluxo real completo e só então avançar para integrações grandes.

## Direções funcionais já decididas
### 1. Browser / web para o agente
O agente do OpenChatCut deve futuramente ter acesso a navegador/web via Playwright/MCP ou equivalente para:
- pesquisar web;
- localizar recursos;
- baixar/importar mídia permitida;
- trabalhar de forma headless por padrão, com painel/visibilidade quando útil.

Regra legal: localizar conteúdo é uma coisa; baixar/reutilizar música ou mídia protegida comercialmente sem permissão é outra. Nunca tratar copyright como autorização automática.

### 2. Provider multimodal unificado
Meta:
- cadastrar um provedor uma vez;
- detectar capacidades (chat/texto, imagem, vídeo, áudio, música/SFX etc.);
- não exigir que o mesmo provedor seja configurado várias vezes para modalidades que ele já suporta;
- expor capacidades reais na UI.

### 3. Modo AUTO
O OpenChatCut deve ter roteamento automático por subtarefa:
- detectar rapidamente modelos/capacidades disponíveis;
- escolher o melhor modelo/provedor para a tarefa;
- considerar capacidade, qualidade, latência e custo quando disponível;
- fazer fallback rápido em caso de erro;
- evitar sondagens lentas que prejudiquem a UX.

Exemplos:
- edição de vídeo/proposta -> melhor LLM disponível;
- geração de imagem -> melhor modelo de imagem disponível;
- vídeo/frames -> modelo de vídeo disponível;
- voz/ASR/TTS -> provider de áudio;
- música/SFX -> provider de áudio/música.

## Estado visual / design
O estado visual atual do editor local não é o objetivo final. O usuário explicitamente considera o visual atual simples, feio e bugado.

A direção futura do design é usar como referência principal o conjunto de screenshots do OpenChatCut em:
`assets/readme-pic/`
com destaque para:
- `01-editor-overview.png`
- `02-project-dashboard.png`
- `03-agent-transitions.png`
- `04-motion-graphics.png`
- `05-effects.png`
- `06-zoom.png`
- `07-lut.png`

Essas imagens devem ser tratadas como referência visual/UX para a futura reconstrução do layout, não como desculpa para copiar cegamente código ou ignorar a arquitetura atual.

## Próxima grande sequência
1. Fechar o 401/config do LLM no app real.
2. Rodar E2E real completo.
3. Consolidar estado em commit seguro.
4. Fazer auditoria visual/UX do editor atual.
5. Redesenhar o editor para a referência visual definida pelo usuário.
6. Integrar browser/Playwright no agente.
7. Implementar provider multimodal unificado + capability discovery.
8. Implementar AUTO routing/fallback.
9. Revalidar tudo com testes + fluxo manual.
