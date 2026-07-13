---
name: instalar-paperclip
description: Guia de instalação do Paperclip passo a passo. Método principal, pedir para o Claude Code instalar sozinho (via https://paperclip.ing/llms.txt). Detecta o sistema operacional (Mac, Windows ou Linux) e a forma de autenticação. Use quando o usuário pedir para "instalar o Paperclip", "configurar o Paperclip", "rodar o Paperclip", "colocar o Paperclip pra funcionar", "montar minha empresa digital", ou disser que não sabe instalar / travou na instalação do Paperclip.
---

# Instalar o Paperclip (instalador guiado)

Você guia a pessoa a instalar e rodar o Paperclip, do zero até a tela inicial no `http://localhost:3100`. O jeito mais fácil (e mais no espírito "sem programar") é **pedir para o Claude Code instalar sozinho**. Fale simples, um passo de cada vez, confirme cada etapa.

## Passo 0 — Descobrir o contexto
Pergunte (se ainda não souber):
1. **Sistema operacional:** Mac, Windows ou Linux?
2. A pessoa **já tem o Claude Code** instalado? (Se não, Passo 1.)
3. **Autenticação:** usar a **assinatura Claude** (mais fácil, sem cartão) ou uma **API key** própria (paga por uso)? Recomende a assinatura para quem está testando.

## Passo 1 — Ter o Claude Code
O **Claude Code** é o Claude que faz coisas no computador — é ele que vai instalar o Paperclip pra pessoa.

- **Recomendado (sem terminal):** baixar o **app do Claude** em https://claude.com/download, instalar e abrir. O Claude Code já vem dentro do app, numa **janela** — sem linha de comando. Ideal pra público iniciante.
- **Alternativa (terminal, avançado):** `curl -fsSL https://claude.ai/install.sh | bash` (Mac/Linux/WSL); conferir com `claude --version`.
- **Login (assinatura):** entrar com a conta Pro/Max (um clique no app). Garantir que **não** há `ANTHROPIC_API_KEY` no ambiente (senão vira cobrança por uso).

## Passo 2 — Método fácil: pedir para o Claude instalar
Com o Claude Code aberto (na janela do **app**, sem terminal), a pessoa escreve:

```
Please install paperclip https://paperclip.ing/llms.txt
```

O `llms.txt` é um manual legível por IA. O Claude Code lê, entende que precisa rodar o onboarding e **instala o Paperclip sozinho**, pedindo confirmação quando necessário. Funciona igual em Mac, Windows e Linux, porque quem executa é o Claude Code. Ao terminar, abre em `http://localhost:3100`.

## Passo 2b — Método manual (alternativa / se a pessoa não usa Claude Code)
- **Mac:** app desktop — baixar o `.dmg` (Apple Silicon = `arm64`) em https://github.com/aronprins/paperclip-desktop/releases/latest → arrastar pra Aplicativos → abrir (botão direito → Abrir na 1ª vez) → modo **Local**.
- **Windows/Linux:** instalar Node.js 20+ (https://nodejs.org), habilitar pnpm (`corepack enable`) e rodar (⚠️ **sem** `sudo`):
  ```
  npx paperclipai onboard --yes
  ```
  Rodar de novo depois: `npx paperclipai run`.

## Passo 3 — Autenticação no Paperclip
- **Assinatura (recomendado, sem API key):** ao criar o agente, escolher o adapter **Claude Code** — ele usa o login do `claude`. Custo de API = $0.
- **API key (paga):** criar em https://console.anthropic.com → API Keys → Create Key (`sk-ant-...`) e colar no adapter/secrets.

## Passo 4 — Verificar
- Abrir `http://localhost:3100` (tela de criar empresa).
- Opcional: `curl http://localhost:3100/api/health` → `{"status":"ok"}`.

## Passo 5 — Primeiros passos
Criar **New Company** (missão) → **Add agent** (adapter Claude Code) → definir **budget** → montar os setores → criar **missão → objetivo → tarefa**.

## Erros comuns
- **"Embedded PostgreSQL failed / administrative user"** → rodou como root/sudo. Rodar como usuário normal.
- **`node`/`claude` não encontrado** → instalar Node 20+ / Claude Code.
- **Trava pedindo API key** → escolher o adapter **Claude Code** (a autenticação vem do `claude login`).
- **Diagnóstico:** `npx paperclipai doctor` (`--repair` conserta o que dá).

## Regras
- Nunca rode instalação com `sudo`/root.
- Sempre avise sobre **custo/uso** antes de rodar agentes.
- Explique cada passo em linguagem simples; a pessoa pode não ser técnica.
- Só execute comandos depois de dizer o que fazem e a pessoa confirmar.
