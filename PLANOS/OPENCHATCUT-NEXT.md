# Próximos passos — OpenChatCut

## Fase 0 — Fechar a base
### P0.1
Corrigir a resolução do provider/API no dev server e remover a causa do 401 real do app.

### P0.2
Reiniciar servidor depois da configuração e repetir:
- chat;
- proposta de edição;
- aplicação da proposta;
- alteração real da timeline;
- persistência/reload;
- cancelamento;
- exportação quando aplicável.

### P0.3
Rodar a suíte de verify/E2E novamente e registrar evidência.

## Fase 1 — Consolidar
- revisar mudanças locais;
- criar checkpoint/commit limpo;
- atualizar memória;
- só depois publicar/push quando for a decisão.

## Fase 2 — Redesign
Objetivo: transformar o editor atual no nível visual/UX da referência de `assets/readme-pic/01...07`.

Ordem sugerida:
1. shell/layout principal;
2. agent/chat panel;
3. media pool/library;
4. preview;
5. multitrack timeline;
6. inspectors/settings;
7. typography/spacing/surface hierarchy;
8. states/empty/loading/error;
9. responsive/desktop behavior;
10. motion/microinteractions;
11. visual regression.

Não alterar comportamento de edição só para conseguir o visual.

## Fase 3 — Browser
Adicionar Playwright/MCP com:
- pesquisa;
- navegação;
- seleção de fontes;
- download de mídia permitida;
- importação para media pool;
- execução headless por padrão;
- opção de observar a atividade.

Testar timeout, cancelamento, segurança, tamanho de arquivo, tipos MIME e origem.

## Fase 4 — Multimodal providers
Criar capability registry:
- text/chat
- vision/image input
- image generation
- video generation
- speech-to-text
- text-to-speech
- music
- sound effects
- embeddings/other quando necessário.

Uma credencial/provedor pode expor múltiplas capabilities.

## Fase 5 — AUTO
Pipeline:
1. detectar capability necessária;
2. obter candidatos;
3. health/probe curto;
4. rankear;
5. executar;
6. fallback se falhar;
7. registrar resultado e motivo.

Nunca fazer um probe longo antes de cada ação.

## Fase 6 — Qualidade final
- testes de integração;
- testes visuais;
- testes de recuperação;
- testes de cancelamento;
- testes de persistência;
- auditoria de segredos;
- fluxo completo em Windows;
- smoke test do navegador/MCP;
- smoke test multimodal.
