# Mozg

**Русский** · [English](#english)

Mozg — ИИ-агент для работы с кодом в терминале. Читает и правит файлы проекта, запускает
команды (с вашего разрешения), ищет по коду и объясняет его. Работает на моделях вашей подписки
Mozg AI: вход — через аккаунт Mozg AI, расход идёт из пакета подписки.

**Раньше назывался Mori Code** (до версии 0.2.0, команда `mori`). Команда теперь — `mozg`, а `mori`
установщик оставляет синонимом: старые скрипты работают, настройки и история сессий сохраняются.
Сервис переехал на **mozg.world**, поэтому после обновления один раз войдите заново: `mozg login`.

Подробнее и тарифы: **https://mozg.world/code**

Этот репозиторий — только для загрузок: здесь лежат готовые сборки и контрольные суммы.
Исходного кода здесь нет.

## Что нужно

- **Платный тариф Mozg AI** (на бесплатном Mozg недоступен).
- macOS 11+ (Apple Silicon или Intel), Linux x64/arm64 с glibc (Ubuntu 20.04+, Debian 11+, Fedora и
  т.п.; Alpine/musl пока нет), Windows 10/11 x64.

## Установка

macOS и Linux:

```bash
curl -fsSL https://mozg.world/code/install.sh | bash
```

Windows (PowerShell):

```powershell
irm https://mozg.world/code/install.ps1 | iex
```

Если `mozg.world` у вас ещё не открывается — те же установщики из этого репозитория:
`curl -fsSL https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest/download/install.sh | bash`,
`irm https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest/download/install.ps1 | iex`.

Установщик сам выбирает сборку под систему, сверяет контрольную сумму (SHA-256) и кладёт `mozg`
(и синоним `mori`) в `~/.local/bin` (Windows — `%LOCALAPPDATA%\mozg\bin`, папка добавляется в PATH;
если Mori Code уже стоял в `%LOCALAPPDATA%\mori\bin`, обновление ставится туда же). Права
администратора не нужны. Конкретная версия: `MORI_VERSION=0.2.0`, другая папка:
`MORI_INSTALL_DIR=...`. Обновление — тот же установщик ещё раз.

Затем:

```bash
mozg login            # откроется браузер → «Разрешить»
mozg login --device   # по SSH или без браузера: код вводится на любом устройстве
mozg status           # проверить вход и список моделей
mozg                  # запустить агента в папке проекта
```

В VS Code, Cursor и других редакторах запускайте `mozg` во встроенном терминале.

## Ручная установка

Скачайте архив под свою систему со страницы
[последнего релиза](https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest) и
проверьте сумму по `SHA256SUMS.txt`:

| Система | Файл |
|---|---|
| macOS Apple Silicon | `mozg-<версия>-darwin-arm64.tar.gz` |
| macOS Intel | `mozg-<версия>-darwin-x64.tar.gz` |
| Linux x64 | `mozg-<версия>-linux-x64.tar.gz` |
| Linux arm64 | `mozg-<версия>-linux-arm64.tar.gz` |
| Windows x64 | `mozg-<версия>-windows-x64.zip` |

До версии 0.2.0 архивы назывались `mori-code-<версия>-…`, а бинарник в них — `mori`.

```bash
shasum -a 256 -c SHA256SUMS.txt --ignore-missing     # Linux: sha256sum -c ... --ignore-missing
mkdir -p ~/.local/bin && tar -xzf mozg-*-darwin-arm64.tar.gz -C ~/.local/bin mozg
ln -sf mozg ~/.local/bin/mori                        # по желанию: старое имя команды
```

**macOS: «не удаётся проверить разработчика».** Файл, скачанный браузером, получает метку
карантина, а сборки пока не нотаризованы Apple. Снимите метку:

```bash
xattr -d com.apple.quarantine ~/.local/bin/mozg
```

Установщик через `curl` этой проблемы не имеет: `curl` метку не ставит.

**Windows: SmartScreen.** Сборка пока не подписана; если Windows предупредит при первом запуске
вручную скачанного `mozg.exe`, нажмите «Подробнее» → «Выполнить в любом случае» или выполните
`Unblock-File mozg.exe`.

## Лицензия

Mozg основан на [OpenCode](https://github.com/anomalyco/opencode) (MIT). Текст лицензии — в
[LICENSE](LICENSE), атрибуция — в [NOTICE](NOTICE); оба файла лежат и в каждом архиве.

---

<a id="english"></a>

# Mozg (English)

Mozg is an AI coding agent for your terminal. It reads and edits project files, runs commands
(with your permission), searches and explains code. It runs on the models of your Mozg AI
subscription: you sign in with your Mozg AI account and usage comes out of your subscription package.

**Formerly Mori Code** (before 0.2.0, command `mori`). The command is now `mozg`; the installer keeps
`mori` as an alias, so existing scripts keep working and your settings and sessions are preserved.
The service moved to **mozg.world**, so sign in once more after updating: `mozg login`.

Details and plans: **https://mozg.world/code**

This repository only hosts downloads (release builds and checksums). There is no source code here.

## Requirements

- **A paid Mozg AI plan** (Mozg is not available on Free).
- macOS 11+ (Apple Silicon or Intel), Linux x64/arm64 with glibc (Ubuntu 20.04+, Debian 11+,
  Fedora, …; no Alpine/musl yet), Windows 10/11 x64.

## Install

macOS and Linux:

```bash
curl -fsSL https://mozg.world/code/install.sh | bash
```

Windows (PowerShell):

```powershell
irm https://mozg.world/code/install.ps1 | iex
```

If `mozg.world` does not open for you yet, use the same installers from this repository:
`curl -fsSL https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest/download/install.sh | bash`,
`irm https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest/download/install.ps1 | iex`.

The installer picks the build for your system, verifies its SHA-256 checksum and puts `mozg` (plus
the `mori` alias) into `~/.local/bin` (Windows: `%LOCALAPPDATA%\mozg\bin`, added to your user PATH;
an existing Mori Code install in `%LOCALAPPDATA%\mori\bin` is updated in place). No admin rights
needed. Pin a version with `MORI_VERSION=0.2.0`, choose a folder with `MORI_INSTALL_DIR=...`.
To update, run the installer again.

Then:

```bash
mozg login            # opens the browser → "Allow"
mozg login --device   # over SSH / without a browser: enter the code on any device
mozg status           # check sign-in and your models
mozg                  # start the agent in your project folder
```

In VS Code, Cursor and other editors, run `mozg` in the integrated terminal.

## Manual install

Download the archive for your system from the
[latest release](https://github.com/MORI-AI-PLATFORM/mori-code-releases/releases/latest) (see the
table above; before 0.2.0 the archives were named `mori-code-<version>-…` with a `mori` binary) and
verify it against `SHA256SUMS.txt`.

**macOS "cannot verify the developer".** Browser downloads get a quarantine flag and the builds are
not notarized yet. Remove the flag: `xattr -d com.apple.quarantine ~/.local/bin/mozg`. The `curl`
installer is not affected: `curl` does not set the flag.

**Windows SmartScreen.** The build is not code-signed yet. If Windows warns on first run of a
manually downloaded `mozg.exe`, choose "More info" → "Run anyway", or run `Unblock-File mozg.exe`.

## License

Mozg is based on [OpenCode](https://github.com/anomalyco/opencode) (MIT). See
[LICENSE](LICENSE) and [NOTICE](NOTICE); both also ship inside every archive.
