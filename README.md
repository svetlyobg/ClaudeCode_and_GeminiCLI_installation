# Инсталиране на Claude Code и Gemini CLI на Windows

## 1. Инсталиране на Node.js

Claude Code изисква **Node.js 18+**, а Gemini CLI изисква **Node.js 20+**. Препоръчително е да инсталирате последната **LTS** версия, за да покриете и двете изисквания.

1. Отворете [https://nodejs.org](https://nodejs.org)
2. Изтеглете **LTS** версията за Windows
3. Стартирайте инсталатора и следвайте стъпките (настройките по подразбиране са достатъчни)
4. След инсталацията отворете **PowerShell** като Администратор и проверете:

```powershell
node -v
npm -v
```

Ако и двете команди върнат версия, Node.js е инсталиран успешно.

---

## 2. Инсталиране на Claude Code

### Инсталация

```powershell
npm install -g @anthropic-ai/claude-code
```

### Стартиране

```powershell
Set-ExecutionPolicy Bypass -Scope Process; claude
```

> **Забележка:** `Set-ExecutionPolicy Bypass -Scope Process` временно разрешава изпълнението на скриптове само за текущата PowerShell сесия. Това е необходимо, защото Windows по подразбиране блокира изпълнението на скриптове.

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
