# Ocean Agents — desafio final do bootcamp

Sistema multiagente (LangGraph + MCP + RAG) que controla a frota de 4 navios do Porto Alfa.

## Como rodar na sua máquina (Windows / PowerShell)

```powershell
git clone https://github.com/<dono>/<repositorio>.git
cd <repositorio>
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
copy .env.example .env      # depois abra o .env e preencha suas chaves
```

Se o PowerShell bloquear o `Activate.ps1`, rode uma vez:
`Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`

Executar:

```powershell
python mcp_server/server.py   # terminal 1: servidor MCP
python -m src.app.main        # terminal 2: agentes
```

## Estrutura

```text
src/
  app/          # entrada do programa (main.py, interface Streamlit)
  graph/        # state.py, builder.py, routing.py, tools.py
    nodes/      # um arquivo por nó
    prompts/    # um arquivo por prompt (nunca prompt dentro do nó)
  utils/        # llm_adapter, langfuse_client, mcp_client, vector_store
mcp_server/     # servidor MCP (serviço separado)
scripts/        # testes manuais, avaliação (avaliar.py)
tests/          # cenários automatizados
dados/          # documentos e JSONs do desafio
docs/           # diagrama de arquitetura, apresentação
```

## Quem cuida do quê

| Área | Pastas | Responsável |
|---|---|---|
| Agentes e grafo | `src/graph/` | |
| MCP, simulador e testes | `mcp_server/`, `src/utils/mcp_client.py`, `tests/`, `scripts/` | |
| RAG e dados | `src/utils/vector_store.py`, `dados/` | |
| Apresentação e métricas | `docs/`, `src/app/` | |

Como trabalhar no repositório: veja [CONTRIBUTING.md](CONTRIBUTING.md).
