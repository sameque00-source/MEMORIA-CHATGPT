# Provedores e IA — OpenChatCut

## Gateway atualmente usado no trabalho
- Gateway: CodeJato
- Base Anthropic compatível: `https://api.tn1.top/v1`
- Modelo testado: `claude-opus-5-5`
- Resultado externo observado: HTTP 200 com identificação do modelo.

## Preferência de Claude
Configuração de trabalho definida:
- modelo: Opus 5.5
- contexto: 1M
- esforço: Máximo

## Variáveis do harness de E2E já observadas
O harness usa:
- `OPENCHATCUT_E2E_LLM_API_KEY`
- `OPENCHATCUT_E2E_LLM_PROVIDER`
- `OPENCHATCUT_E2E_LLM_BASE_URL`
- `OPENCHATCUT_E2E_LLM_MODEL`
- `OPENCHATCUT_E2E_LLM_API_MODE`

## Variáveis do app/provedor
A resolução real do app usa slots de provider, incluindo a família:
- `LLM_ANTHROPIC_COMPATIBLE_API_KEY`
- demais campos correspondentes do slot.

Havia entradas antigas `LLM_CUSTOM_1/2/3_*` com URLs localhost e o dev server não estava recebendo a mesma configuração válida do harness.

## Segurança
Nunca registrar a chave real aqui. Rotacionar uma chave caso ela tenha sido exposta em conversa/log.


## Atualização pós-formatação — 2026-10-11

- O PC foi formatado. O backup global privado `sameque00-source/claude-code-global-backup` inclui `codejato_key.py`, configurações e restaurador, mas **não** inclui a chave real.
- O restaurador pede a chave por entrada oculta e grava localmente em `%USERPROFILE%\\.codejato\\chave-codejato.txt` com ACL restrita. Inserir a chave apenas nesse prompt, nunca nesta memória pública.
- O relatório de segurança do backup diz que o plano CodeJato foi limitado aos apps Claude e que chamadas HTTP diretas de scripts receberam 403. Testar primeiro pelo próprio Claude Code e usar o `VERIFY-RESTORE.ps1` em PowerShell normal.
- Antes de configurar OpenChatCut, inspecionar a construção exata da URL e o protocolo requerido pelo provider. Há referências históricas à base `https://api.tn1.top` e à base `https://api.tn1.top/v1`; não concatenar/remover `/v1` por tentativa aleatória.
- O alias `claude-opus-5-5` e um `modelUsage` informado pelo gateway não comprovam qual modelo remoto respondeu.
- FreeLLMAPI é uma tarefa opcional e separada. Não há prova de que elimine limites oficiais da assinatura Claude. Não executar `curl | bash` diretamente no PowerShell; primeiro inspecionar o script e confirmar ambiente/runtime suportado.
