# Decisões consolidadas — OpenChatCut

## D1 — Estabilizar antes de expandir
Primeiro fechar bugs e validar o caminho real do app. Depois browser/MCP multimodal/AUTO e redesign.

## D2 — Local-first
Projetos e mídia devem continuar locais por padrão. Serviços cloud só recebem o necessário para a tarefa configurada.

## D3 — Uma configuração por provedor quando possível
Se um provedor oferece texto + imagem + vídeo + áudio em uma integração coerente, registrar uma vez e detectar capacidades automaticamente.

## D4 — AUTO routing
O sistema deve selecionar modelos por subtarefa, sem exigir que o usuário escolha manualmente a cada operação. A seleção deve ser rápida e ter fallback.

## D5 — Browser do agente
Acesso web deve vir por integração explícita de browser/MCP (por exemplo Playwright). O agente não deve fingir que tem web se a ferramenta não estiver instalada.

## D6 — Segurança de mídia
O agente pode pesquisar e trabalhar com fontes permitidas. Conteúdo protegido por copyright não ganha licença de reutilização apenas por estar disponível online.

## D7 — Visual futuro
O redesign deve mirar o conjunto de screenshots do Product Tour do OpenChatCut, especialmente `01-editor-overview.png` a `07-lut.png`. Não fazer o redesign antes da estabilização funcional.

## D8 — Não expor segredos
Memória pública nunca deve conter API keys, tokens, cookies, senhas ou credenciais.
