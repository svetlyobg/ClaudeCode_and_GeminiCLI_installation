# Инсталиране на Claude Code и Gemini CLI на Windows

## 1. Инсталиране на Node.js

Claude Code изисква **Node.js 18+**, а Gemini CLI изисква **Node.js 20+**. Препоръчително е да инсталирате последната **LTS** версия, за да покриете и двете изисквания.

1. Отворете [https://nodejs.org](https://nodejs.org)
2. Изтеглете **LTS** версията за Windows
3. Стартирайте инсталатора и следвайте стъпките (настройките по подразбиране са достатъчни)
4. След инсталацията отворете **PowerShell** като Администратор и проверете:

```powershell
node -v
```

```powershell
npm -v
```

Ако и двете команди върнат версия, Node.js е инсталиран успешно.

---

## 2. Инсталиране на Claude Code

### Инсталация

**Начин 1 — чрез npm (препоръчително):**

```powershell
npm install -g @anthropic-ai/claude-code
```

**Начин 2 — чрез winget (Windows Package Manager):**

```powershell
winget install Anthropic.ClaudeCode
```

> **winget** е вграденият мениджър на пакети на Windows (наличен на Windows 10 1709+ и Windows 11). Не изисква предварително инсталиран Node.js — всичко необходимо се инсталира автоматично. Подходящ избор, ако предпочитате по-опростена инсталация без допълнителни зависимости.

Очакван изход при инсталация чрез winget:

```
Found Claude Code [Anthropic.ClaudeCode] Version 2.1.62
This application is licensed to you by its owner.
Microsoft is not responsible for, nor does it grant any licenses to, third-party packages.
Downloading https://storage.googleapis.com/.../claude.exe
  ██████████████████████████████   225 MB /  225 MB
Successfully verified installer hash
Starting package install...
Command line alias added: "claude"
Path environment variable modified; restart your shell to use the new value.
Successfully installed
```

> **Забележка след winget инсталация:** Съобщението `Path environment variable modified; restart your shell to use the new value.` означава, че трябва да **затворите и отворите отново PowerShell**, преди да можете да стартирате `claude`.

Очакван изход след успешна инсталация чрез npm:

```
PS C:\WINDOWS\system32> npm install -g @anthropic-ai/claude-code
added 2 packages in 9s
1 package is looking for funding
  run `npm fund` for details
npm notice
npm notice New minor version of npm available! 11.9.0 -> 11.11.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.11.0
npm notice To update run: npm install -g npm@11.11.0
npm notice
PS C:\WINDOWS\system32>
```

> **За съобщението `npm notice New minor version of npm available!`:**
> npm ви уведомява, че има нова версия на самия npm (мениджъра на пакети). Това **не е грешка** — Claude Code е инсталиран успешно. Ако искате да обновите npm, изпълнете отделно:
>
> ```powershell
> npm install -g npm@11.11.0
> ```
>
> Това обновява **самия npm**, а не Claude Code. Препоръчително е да го направите, за да имате последните подобрения и поправки на сигурността в мениджъра на пакети.

### Стартиране

```powershell
Set-ExecutionPolicy Bypass -Scope Process; claude
```

> **Забележка:** `Set-ExecutionPolicy Bypass -Scope Process` временно разрешава изпълнението на скриптове само за текущата PowerShell сесия. Това е необходимо, защото Windows по подразбиране блокира изпълнението на скриптове.

При първото стартиране може да видите следния изход:

```
PS C:\Users\Svet\...> Set-ExecutionPolicy Bypass -Scope Process; claude

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution
policy might expose you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): a

Claude Code on Windows requires git-bash (https://git-scm.com/downloads/win). If installed but not
in PATH, set environment variable pointing to your bash.exe, similar to:
CLAUDE_CODE_GIT_BASH_PATH=C:\Program Files\Git\bin\bash.exe
```

**Обяснение на стъпките:**

**1. Въпросът за execution policy** — Windows пита дали да промени политиката за изпълнение на скриптове. Въведете `a` (Yes to All), за да потвърдите. Това е безопасно, тъй като `Bypass -Scope Process` важи **само за текущата сесия** и се нулира при затваряне на PowerShell.

**2. Съобщението за git-bash** — Claude Code на Windows изисква **Git Bash** като среда за изпълнение. Ако виждате това съобщение:

- Изтеглете и инсталирайте Git за Windows от [https://git-scm.com/downloads/win](https://git-scm.com/downloads/win)
- След инсталацията опитайте отново. Ако проблемът продължава, задайте системна променлива:

```powershell
$env:CLAUDE_CODE_GIT_BASH_PATH = "C:\Program Files\Git\bin\bash.exe"
```

или добавете постоянно чрез системните настройки на Windows:

```
Променлива: CLAUDE_CODE_GIT_BASH_PATH
Стойност:   C:\Program Files\Git\bin\bash.exe
```

При първото стартиране Claude Code ще ви поиска да влезете в акаунта си в Anthropic или да въведете API ключ.

### Режим на безопасност

Често срещана употреба в неинтерактивен/автоматизиран режим:

`claude -p --dangerously-skip-permissions "вашата подкана тук"`

> **Забележка:** Използвайте това внимателно — то заобикаля всички подкани за безопасност, така че Claude ще изпълнява редакции и команди без да иска одобрение.

---

## 3. Инсталиране на Gemini CLI

### Инсталация

```powershell
npm install -g @google/gemini-cli
```

### Стартиране

```powershell
Set-ExecutionPolicy Bypass -Scope Process; gemini
```

При първото стартиране Gemini CLI ще ви поиска да влезете с Google акаунт.

> **Безплатен план:** Gemini CLI предлага безплатен план с личен Google акаунт -- 60 заявки/мин и 1000 заявки/ден.

---

## Полезни команди

| Команда | Описание |
|---------|----------|
| `claude` | Стартира Claude Code |
| `claude /help` | Показва помощ за Claude Code |
| `gemini` | Стартира Gemini CLI |
| `npm update -g @anthropic-ai/claude-code` | Обновява Claude Code |
| `npm update -g @google/gemini-cli` | Обновява Gemini CLI |

---

## Отстраняване на проблеми

- **"npm is not recognized"** -- Node.js не е инсталиран или не е добавен в PATH. Преинсталирайте Node.js.
- **"Execution policy"** грешка -- Използвайте `Set-ExecutionPolicy Bypass -Scope Process` преди командата.
- **Проблеми с версията** -- Уверете се, че имате Node.js 18+: `node -v`

### ✗ Auto-update failed

Ако видите съобщението:

```
✗ Auto-update failed · Try claude doctor or npm i -g @anthropic-ai/claude-code
```

**Как да поправите:**

1. Стартирайте диагностиката:
   ```powershell
   claude doctor
   ```
2. Или преинсталирайте ръчно:
   ```powershell
   npm i -g @anthropic-ai/claude-code
   ```
