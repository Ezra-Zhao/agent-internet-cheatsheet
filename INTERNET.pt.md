# 🌐 Internet para seu Agente de IA (Português)

> Comandos verificados com o README de [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) (2026-10-09).
> Ideia central: é uma "camada de capacidade" — escolhe, instala e monitora a forma mais estável de acessar cada plataforma. Se um caminho quebra, troca para o próximo sem você fazer nada.

---

## 0. Instalação: uma frase

Cole isto no seu agente (Claude Code / Cursor / OpenClaw / Windsurf, qualquer um que rode comandos):

```
帮我安装 Agent Reach：https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/install.md
```

Em minutos ele lê Twitter, busca no Reddit, assiste YouTube e navega no Xiaohongshu. Para atualizar:

```
帮我更新 Agent Reach：https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/update.md
```

Prévia sem mexer no sistema: `agent-reach install --dry-run`

---

## 1. Pronto sem configuração (sem login)

| Plataforma | Comando / uso | Notas |
|---|---|---|
| Qualquer site | `curl https://r.jina.ai/URL` | Jina Reader, grátis, sem API key, retorna texto limpo |
| YouTube | `yt-dlp --write-subs --write-auto-subs --sub-langs "pt.*,en.*" --skip-download "URL"` | Extrai legendas para o agente "assistir" ao vídeo |
| GitHub público | `gh repo view owner/repo` | Lê descrição/README; busque com `gh search` |
| Bilibili | `bili search "palavra-chave"` | Busca sem login (yt-dlp está bloqueado pelo Bilibili) |
| RSS/Atom | `python3 -c "import feedparser; d=feedparser.parse('URL_RSS'); print([e.title for e in d.entries[:5]])"` | Assine e o agente verifica sozinho |
| V2EX | Canal sem configuração | Posts populares, por nó, detalhe + respostas |
| Xueqiu | Canal sem configuração | Cotações, buscar ações, posts populares |
| Busca na web | Busca semântica Exa (via MCP, sem key) | Configura sozinho na instalação |

---

## 2. Com login (diga uma frase ao agente e ele guia você)

| Plataforma | Como desbloquear | O que dá para fazer |
|---|---|---|
| Twitter/X | Diga «帮我配 Twitter», exporte o cookie com Cookie-Editor | Ler tweets → buscar, timeline, threads longos |
| Reddit | OpenCLI (desktop) ou `rdt-cli` | Via anônima bloqueada: login obrigatório |
| Xiaohongshu | OpenCLI (reusa sua sessão do Chrome já aberta) | Buscar, ler, comentar; o agente não faz login por você |
| Facebook | OpenCLI (sessão do navegador) | Buscar, páginas, feed, grupos |
| Instagram | OpenCLI (sessão do navegador) | Buscar usuários, perfil, posts recentes, Explore |
| LinkedIn | Jina Reader para páginas públicas | Perfil, páginas de empresas, buscar vagas |
| GitHub privado | Diga «帮我登录 GitHub» | Repos privados, issues, PRs, forks |

---

## 3. Diagnóstico e manutenção

```bash
agent-reach doctor              # Qual canal funciona? Qual backend usa? Como consertar?
agent-reach install --dry-run   # Prévia antes de instalar
agent-reach uninstall           # Desinstala: limpa ~/.agent-reach/, skills e MCP
agent-reach uninstall --keep-config  # Só apaga skills, guarda tokens
```

**Modelo mental:** cada plataforma = lista ordenada "preferido + alternativo". Se bloquearem um caminho, muda a ordem — o `doctor` sempre diz qual está ativo.

---

## 4. Cenários reais

| Cenário | Canais | Em uma frase |
|---|---|---|
| Monitorar marca | Twitter/X + Xiaohongshu | Busca seu produto todo dia; o agente resume em 5 linhas |
| Pesquisa técnica | Legendas YouTube/Bilibili + GitHub | 3 vídeos + 2 READMEs → relatório comparativo |
| Seguir concorrentes | GitHub releases + RSS | Assine os releases rivais; ele avisa você |
| Pulso do setor | LinkedIn vagas + Xueqiu + V2EX | Revisão semanal; o agente extrai o importante |
| Base de conhecimento | Jina Reader | Baixa a documentação e alimenta seu RAG |

---

## 5. Linha vermelha de segurança

- **Contas secundárias para cookies**: Twitter/Xiaohongshu via cookie podem detectar automação e banir — use conta secundária, nunca a principal.
- **Credenciais só no local**: cookies/tokens em `~/.agent-reach/config.yaml` (permissão 600), nada é enviado.
- **Não mexe no sistema por padrão**: só `--system` instala dependências e escreve configuração.

---

*O upstream muda rápido; na dúvida, rode `agent-reach doctor`.*
