# Como trabalhar neste repositório

## Regras do time

1. **Ninguém faz push direto na `main`.** Tudo entra por Pull Request (PR).
2. **Toda PR é revisada por mais uma pessoa** antes do merge.
3. **Nunca suba o `.env`** nem cole chaves de API em código, prompt ou print.
4. **PRs pequenas e frequentes.** Melhor 3 PRs por dia do que 1 gigante no fim.
5. **Cada um mexe na sua área** (veja a tabela no README). Precisa alterar um arquivo de outra área? Avise no grupo antes.
6. **Puxe a `main` atualizada** antes de começar qualquer tarefa.

## Configuração (uma vez só)

```powershell
git config --global user.name "Seu Nome"
git config --global user.email "email-da-sua-conta-github@exemplo.com"
```

Aceite o convite do repositório (chega por e-mail ou em github.com/notifications) e clone. Na primeira vez que fizer push, o Git abre o navegador para você entrar no GitHub.

## Fluxo de cada tarefa

```powershell
# 1. Atualizar a main
git switch main
git pull

# 2. Criar uma branch para a tarefa
git switch -c feat/revisor-action-hash

# 3. Trabalhar e salvar em commits pequenos
git status
git add src/graph/nodes/revisor.py
git commit -m "revisor valida action_hash da proposta"

# 4. Enviar a branch
git push -u origin feat/revisor-action-hash
```

5. No GitHub, clique em **Compare & pull request**, descreva o que mudou e como testar, e peça revisão a alguém.
6. O revisor comenta ou aprova. Depois de aprovada, clique em **Squash and merge** e em **Delete branch**.
7. Todo mundo atualiza: `git switch main` e `git pull`.

### Nomes de branch

| Prefixo | Para quê | Exemplo |
|---|---|---|
| `feat/` | funcionalidade nova | `feat/mcp-set-speed` |
| `fix/` | correção | `fix/eta-tempestade` |
| `docs/` | documentação, apresentação | `docs/diagrama-arquitetura` |
| `test/` | cenários de teste | `test/falha-motor-s4` |

## A main andou enquanto eu trabalhava

Traga as novidades para a sua branch antes de abrir (ou atualizar) a PR:

```powershell
git switch main
git pull
git switch feat/minha-branch
git merge main
```

### Se der conflito

O Git avisa quais arquivos conflitaram. Abra cada um (o VS Code mostra botões *Accept Current / Accept Incoming / Accept Both*) e resolva os trechos entre `<<<<<<<` e `>>>>>>>`. Depois:

```powershell
git add arquivo-resolvido.py
git commit
git push
```

Na dúvida, **chame a pessoa que escreveu o outro lado do conflito**. Não apague código dos outros para "fazer passar".

## Comandos de socorro

| Situação | Comando |
|---|---|
| Ver o que mudou | `git status` e `git diff` |
| Desfazer alterações não salvas de um arquivo | `git restore arquivo.py` |
| Tirar arquivo do `git add` | `git restore --staged arquivo.py` |
| Corrigir a mensagem do último commit (antes do push) | `git commit --amend` |
| Guardar alterações para trocar de branch | `git stash` e depois `git stash pop` |
| Ver o histórico | `git log --oneline --graph -15` |

**Nunca use `git push --force` na `main`.**

## Subiu o `.env` sem querer?

1. Avise o time na hora.
2. **Revogue a chave** no painel do provedor (OpenAI, Langfuse) e gere outra. Apagar o arquivo não basta: ele continua no histórico.
3. Tire o arquivo do controle de versão: `git rm --cached .env`, faça commit e push.

## Antes da apresentação

Congele a versão que vai ser apresentada:

```powershell
git switch main
git pull
git tag v1.0-apresentacao
git push origin v1.0-apresentacao
```

Se algo quebrar depois, dá para voltar exatamente a esse ponto com `git switch --detach v1.0-apresentacao`.
