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
