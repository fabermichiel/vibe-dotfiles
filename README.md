# Mistral Vibe — Dotfiles

Persoonlijke configuratie van [Mistral Vibe](https://vibe.mistral.ai) — agents, prompts, tool-rechten en budgetlimieten. Clone deze repo naar `~/.vibe/` op een nieuwe PC om dezelfde setup te krijgen.

## 📁 Wat zit erin

| Pad | Beschrijving |
|-----|-------------|
| `config.toml` | Globale config: model, providers, tool permissions, bash allow/denylist, budget |
| `agents/*.toml` | 11 agent-definities (po, architect, developers, testers, reviewer, devops) met tools, rechten en budget |
| `prompts/*.md` | System prompts voor elke agent — de "hersenen" van het team |
| `.gitignore` | Houdt secrets en runtime state uit git |
| `.env.example` | Template voor je API key |
| `trusted_folders.toml.example` | Template voor vertrouwde mappen (per PC verschillend) |

## 🚫 Wat zit er NIET in ( expres)

- `.env` — bevat je `MISTRAL_API_KEY`
- `trusted_folders.toml` — bevat absolute paden van deze machine
- `logs/`, `cache/`, `locks/`, `vibehistory` — runtime state
- `*_cache.json` — gegenereerde caches

## 🖥️ Setup op een nieuwe PC

```bash
# 1. Clone deze repo naar ~/.vibe
cd ~
git clone <repo-url> .vibe

# 2. API key instellen
cp ~/.vibe/.env.example ~/.vibe/.env
# Vul MISTRAL_API_KEY in .env in

# 3. Vertrouwde mappen instellen
cp ~/.vibe/trusted_folders.toml.example ~/.vibe/trusted_folders.toml
# Pas de paden aan naar jouw projectmappen

# 4. Start Vibe
vibe
```

## 🤖 Agent-overzicht

| Agent | Rol | Safety |
|-------|-----|--------|
| `po` | Product Owner — orchestrator | neutral |
| `architect` | Technisch ontwerp | safe |
| `backend-developer` | Backend implementatie | destructive |
| `frontend-developer` | Frontend implementatie | destructive |
| `shared-developer` | Gedeelde types/utils (FE+BE) | destructive |
| `devops` | CI/CD, infra, deployment | destructive |
| `backend-tester` | Backend validatie | neutral |
| `frontend-tester` | Frontend/UX validatie | neutral |
| `shared-tester` | Shared code tests | neutral |
| `system-tester` | End-to-end integratie tests | neutral |
| `reviewer` | Onafhankelijke code review | safe |

## 🔄 Wijzigingen doorvoeren

```bash
cd ~/.vibe
git add -A
git commit -m "Update vibe config"
git push
```
