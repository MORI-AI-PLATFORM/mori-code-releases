# Mori Code

**Русский** · [English](#english)

Mori Code — ИИ-агент для работы с кодом в терминале. Читает и правит файлы проекта, запускает
команды (с вашего разрешения), ищет по коду и объясняет его. Работает на моделях MORI, вход — через
ваш аккаунт MORI, расход идёт из пакета подписки.

Подробнее и тарифы: **https://moriarti.ai/code**

Этот репозиторий — только для загрузок: здесь лежат готовые сборки и контрольные суммы.
Исходного кода здесь нет.

## Что нужно

- **Платный тариф MORI** (на бесплатном Mori Code недоступен).
- macOS 11+ (Apple Silicon или Intel), Linux x64/arm64 с glibc (Ubuntu 20.04+, Debian 11+, Fedora и
  т.п.; Alpine/musl пока нет), Windows 10/11 x64.

## Установка

macOS и Linux:

```bash
curl -fsSL https://moriarti.ai/code/install.sh | bash
```

Windows (PowerShell):

```powershell
irm https://moriarti.ai/code/install.ps1 | iex
```

Установщик сам выбирает сборку под систему, сверяет контрольную сумму (SHA-256) и кладёт `mori`
в `~/.local/bin` (Windows — `%LOCALAPPDATA%\mori\bin`, папка добавляется в PATH). Права
администратора не нужны. Конкретная версия: `MORI_VERSION=0.1.0`, другая папка:
`MORI_INSTALL_DIR=...`.

Затем:

```bash
mori login            # откроется браузер → «Разрешить»
mori login --device   # по SSH или без браузера: код вводится на любом устройстве
mori status           # проверить вход и список моделей
mori                  # запустить агента в папке проекта
```

В VS Code, Cursor и других редакторах запускайте `mori` во встроенном терминале.

## Ручная установка

Скачайте архив под свою систему со страницы
[последнего релиза](https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest) и
проверьте сумму по `SHA256SUMS.txt`:

| Система | Файл |
|---|---|
| macOS Apple Silicon | `mori-code-<версия>-darwin-arm64.tar.gz` |
| macOS Intel | `mori-code-<версия>-darwin-x64.tar.gz` |
| Linux x64 | `mori-code-<версия>-linux-x64.tar.gz` |
| Linux arm64 | `mori-code-<версия>-linux-arm64.tar.gz` |
| Windows x64 | `mori-code-<версия>-windows-x64.zip` |

```bash
shasum -a 256 -c SHA256SUMS.txt --ignore-missing     # Linux: sha256sum -c ... --ignore-missing
mkdir -p ~/.local/bin && tar -xzf mori-code-*-darwin-arm64.tar.gz -C ~/.local/bin mori
```

**macOS: «не удаётся проверить разработчика».** Файл, скачанный браузером, получает метку
карантина, а сборки пока не нотаризованы Apple. Снимите метку:

```bash
xattr -d com.apple.quarantine ~/.local/bin/mori
```

Установщик через `curl` этой проблемы не имеет: `curl` метку не ставит.

**Windows: SmartScreen.** Сборка пока не подписана; если Windows предупредит при первом запуске
вручную скачанного `mori.exe`, нажмите «Подробнее» → «Выполнить в любом случае» или выполните
`Unblock-File mori.exe`.

## Лицензия

Mori Code основан на [OpenCode](https://github.com/anomalyco/opencode) (MIT). Текст лицензии — в
[LICENSE](LICENSE), атрибуция — в [NOTICE](NOTICE); оба файла лежат и в каждом архиве.

---

<a id="english"></a>

# Mori Code (English)

Mori Code is an AI coding agent for your terminal. It reads and edits project files, runs commands
(with your permission), searches and explains code. It runs on MORI models: you sign in with your
MORI account and usage comes out of your subscription package.

Details and plans: **https://moriarti.ai/code**

This repository only hosts downloads (release builds and checksums). There is no source code here.

## Requirements

- **A paid MORI plan** (Mori Code is not available on Free).
- macOS 11+ (Apple Silicon or Intel), Linux x64/arm64 with glibc (Ubuntu 20.04+, Debian 11+,
  Fedora, …; no Alpine/musl yet), Windows 10/11 x64.

## Install

macOS and Linux:

```bash
curl -fsSL https://moriarti.ai/code/install.sh | bash
```

Windows (PowerShell):

```powershell
irm https://moriarti.ai/code/install.ps1 | iex
```

The installer picks the build for your system, verifies its SHA-256 checksum and puts `mori` into
`~/.local/bin` (Windows: `%LOCALAPPDATA%\mori\bin`, added to your user PATH). No admin rights
needed. Pin a version with `MORI_VERSION=0.1.0`, choose a folder with `MORI_INSTALL_DIR=...`.

Then:

```bash
mori login            # opens the browser → "Allow"
mori login --device   # over SSH / without a browser: enter the code on any device
mori status           # check sign-in and your models
mori                  # start the agent in your project folder
```

In VS Code, Cursor and other editors, run `mori` in the integrated terminal.

## Manual install

Download the archive for your system from the
[latest release](https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest) (see the
table above) and verify it against `SHA256SUMS.txt`.

**macOS "cannot verify the developer".** Browser downloads get a quarantine flag and the builds are
not notarized yet. Remove the flag: `xattr -d com.apple.quarantine ~/.local/bin/mori`. The `curl`
installer is not affected: `curl` does not set the flag.

**Windows SmartScreen.** The build is not code-signed yet. If Windows warns on first run of a
manually downloaded `mori.exe`, choose "More info" → "Run anyway", or run `Unblock-File mori.exe`.

## License

Mori Code is based on [OpenCode](https://github.com/anomalyco/opencode) (MIT). See
[LICENSE](LICENSE) and [NOTICE](NOTICE); both also ship inside every archive.
