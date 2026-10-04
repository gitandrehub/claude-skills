# claude-skills

Skill personali per Claude Code.

| Skill | Cosa fa |
|---|---|
| [`explain-code`](skills/explain-code/SKILL.md) | Legge una cartella o un progetto e scrive una guida semplice, step by step, che segue il flusso dall'ingresso all'uscita, con limiti e spunti di miglioramento. |

## Installazione

Clona il repo e collega ogni skill in `~/.claude/skills/`, così un `git pull` aggiorna tutto.

**macOS / Linux**

```sh
git clone https://github.com/gitandrehub/claude-skills.git ~/claude-skills
mkdir -p ~/.claude/skills
for s in ~/claude-skills/skills/*/; do ln -sfn "$s" ~/.claude/skills/"$(basename "$s")"; done
```

**Windows (PowerShell)**

```powershell
git clone https://github.com/gitandrehub/claude-skills.git $HOME\claude-skills
Get-ChildItem $HOME\claude-skills\skills -Directory | ForEach-Object {
  cmd /c mklink /J "$HOME\.claude\skills\$($_.Name)" $_.FullName
}
```

Riavvia Claude Code: le skill compaiono come `/explain-code` ecc.

## Aggiungere una skill

Crea `skills/<nome>/SKILL.md`, rilancia il comando di collegamento, poi commit e push.
