# OpenChatCut

## Visão
Editor de vídeo com IA, local-first, com agente conversacional capaz de ler o estado real do projeto e executar alterações reais na timeline.

## Objetivo do produto
Não é um gerador de vídeo de uso único. Cada ação deve continuar editável: clips, tracks, captions, transitions, effects, keyframes, audio e histórico.

## Stack/arquitetura conhecida
- TypeScript
- React
- Electron/Desktop
- Remotion para preview/renderização
- servidor local para lógica e integrações
- MCP para agentes externos
- ASR/transcrição local e/ou cloud
- sistema de skills e ferramentas do agente
- verify tests para comportamentos críticos

## Repositórios
- Desenvolvimento local: `C:\Users\User\Downloads\Aditor de videos IA\OpenChatCut-ATUAL`
- GitHub do usuário: `sameque00-source/OpenChatCut`
- Repositório-base/original observado: `0xsline/OpenChatCut`

## Direção de produto
- agente + edição manual no mesmo projeto;
- timeline profissional e real;
- projeto local-first;
- edição reversível;
- MCP;
- geração multimodal;
- busca online opcional;
- roteamento automático de modelos;
- integração futura com browser.

## Design
O usuário quer, em uma fase posterior, que a UI deixe de ser simples/bugada e passe a seguir a linguagem visual/UX do conjunto de screenshots do projeto OpenChatCut, especialmente o `01-editor-overview.png` e os screenshots de product tour relacionados.

Arquivos de referência:
`assets/readme-pic/01-editor-overview.png`
`assets/readme-pic/02-project-dashboard.png`
`assets/readme-pic/03-agent-transitions.png`
`assets/readme-pic/04-motion-graphics.png`
`assets/readme-pic/05-effects.png`
`assets/readme-pic/06-zoom.png`
`assets/readme-pic/07-lut.png`

Não tratar a UI atual como design final.

## Regras de engenharia
- preservar o que já funciona;
- mudanças incrementais;
- testes reais;
- nenhum segredo no repositório;
- evitar operações destrutivas;
- não refatorar grandes blocos apenas por estética;
- sempre diferenciar mock/teste de integração real;
- usar agentes/skills somente quando agregarem valor.

## Credenciais
Nunca registrar API keys, tokens, cookies ou senhas nesta memória.
