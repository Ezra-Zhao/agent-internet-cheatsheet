# 🌐 Internet para tu AI Agent (Español)

> Comandos verificados con el README de [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) (2026-10-09).
> Idea clave: es una "capa de capacidad" — elige, instala y revisa la forma más estable de acceder a cada plataforma. Si una vía se rompe, cambia a la siguiente sin que hagas nada.

---

## 0. Instalación: una frase

Copia esto a tu agente (Claude Code / Cursor / OpenClaw / Windsurf, cualquiera que ejecute comandos):

```
帮我安装 Agent Reach：https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/install.md
```

En minutos lee Twitter, busca en Reddit, ve YouTube y navega Xiaohongshu. Para actualizar:

```
帮我更新 Agent Reach：https://raw.githubusercontent.com/Panniantong/agent-reach/main/docs/update.md
```

Vista previa sin tocar el sistema: `agent-reach install --dry-run`

---

## 1. Listo sin configuración (sin login)

| Plataforma | Comando / uso | Notas |
|---|---|---|
| Cualquier web | `curl https://r.jina.ai/URL` | Jina Reader, gratis, sin API key, devuelve texto limpio |
| YouTube | `yt-dlp --write-subs --write-auto-subs --sub-langs "es.*,en.*" --skip-download "URL"` | Extrae subtítulos para que el agente "vea" el video |
| GitHub público | `gh repo view owner/repo` | Lee descripción/README; busca con `gh search` |
| Bilibili | `bili search "palabra clave"` | Busca sin login (yt-dlp está bloqueado por Bilibili) |
| RSS/Atom | `python3 -c "import feedparser; d=feedparser.parse('URL_RSS'); print([e.title for e in d.entries[:5]])"` | Suscríbete y el agente lo revisa solo |
| V2EX | Canal sin configuración | Posts populares, por nodo, detalle + respuestas |
| Xueqiu | Canal sin configuración | Cotizaciones, buscar acciones, posts populares |
| Búsqueda web | Búsqueda semántica Exa (vía MCP, sin key) | Se configura solo al instalar |

---

## 2. Con login (dile una frase a tu agente y te guía)

| Plataforma | Cómo desbloquear | Qué puedes hacer |
|---|---|---|
| Twitter/X | Dile «帮我配 Twitter», exporta la cookie con Cookie-Editor | Leer tweets → buscar, timeline, hilos largos |
| Reddit | OpenCLI (escritorio) o `rdt-cli` | La vía anónima está bloqueada: login obligatorio |
| Xiaohongshu | OpenCLI (reusa tu sesión de Chrome ya abierta) | Buscar, leer, comentar; el agente no inicia sesión por ti |
| Facebook | OpenCLI (sesión del navegador) | Buscar, páginas, feed, grupos |
| Instagram | OpenCLI (sesión del navegador) | Buscar usuarios, perfil, posts recientes, Explore |
| LinkedIn | Jina Reader para páginas públicas | Perfil, páginas de empresa, buscar empleos |
| GitHub privado | Dile «帮我登录 GitHub» | Repos privados, issues, PRs, forks |

---

## 3. Diagnóstico y mantenimiento

```bash
agent-reach doctor              # ¿Qué canal funciona? ¿Qué backend usa? ¿Cómo se arregla?
agent-reach install --dry-run   # Vista previa antes de instalar
agent-reach uninstall           # Desinstala: limpia ~/.agent-reach/, skills y MCP
agent-reach uninstall --keep-config  # Solo borra skills, guarda tokens
```

**Modelo mental:** cada plataforma = lista ordenada "preferido + alternativo". Si bloquean una vía, se cambia el orden — `doctor` siempre te dice cuál está activa.

---

## 4. Escenarios reales

| Escenario | Canales | En una frase |
|---|---|---|
| Monitoreo de marca | Twitter/X + Xiaohongshu | Busca tu producto a diario; el agente resume en 5 líneas |
| Investigación técnica | Subtítulos YouTube/Bilibili + GitHub | 3 videos + 2 READMEs → informe comparativo |
| Seguir competidores | GitHub releases + RSS | Suscríbete a los releases rivales; te avisa |
| Pulso del sector | LinkedIn empleos + Xueqiu + V2EX | Revisión semanal; el agente extrae lo importante |
| Base de conocimiento | Jina Reader | Descarga la documentación y aliméntala a tu RAG |

---

## 5. Línea roja de seguridad

- **Cuentas secundarias para cookies**: Twitter/Xiaohongshu vía cookie pueden detectar automatización y banear — usa una cuenta secundaria, nunca la principal.
- **Credenciales solo en local**: cookies/tokens en `~/.agent-reach/config.yaml` (permiso 600), no se suben.
- **No toca el sistema por defecto**: solo `--system` instala dependencias y escribe configuración.

---

*El upstream cambia rápido; ante la duda, ejecuta `agent-reach doctor`.*
