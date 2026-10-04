# Histórico recente — OpenChatCut

- Foram investigados e corrigidos problemas de relay de texto longo, SSE, stale proposals, Whisper path, seleção de modelo de speech, remove_silence, edição de áudio, cancelamento após restart, escrita de env e isolamento de testes.
- A suíte de verify chegou a exit code 0.
- O gargalo real final identificado foi a configuração do dev server para o provider LLM.
- O redesign visual foi deliberadamente adiado até a base funcional ficar estável.
- As mudanças locais podem estar à frente da branch main do GitHub; sempre conferir o checkout local antes de assumir que tudo está publicado.
