# Инструкция по сборке и установке Antigravity Unlocker

## 1. Где находится исполняемый файл

После сборки исполняемый файл находится по пути:
- **macOS / Linux:** `target/release/ag_unlocker`  
  *(Абсолютный путь на этом компьютере: `/Volumes/1TB/Yandex.Disk.localized/IdeaProjects/work/Antigravity_Unlock/target/release/ag_unlocker`)*
- **Windows:** `target\release\ag_unlocker.exe`

### Запуск на macOS (текущая система):
```bash
# Запуск с графическим интерфейсом (GUI)
./target/release/ag_unlocker

# Или запуск в консольном псевдографическом режиме (TUI)
./target/release/ag_unlocker --tui
```

---

## 2. Что необходимо для сборки

### Общие требования:
1. **Rust и Cargo** (версия 1.80 или новее).
   Установка (macOS / Linux):
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   source "$HOME/.cargo/env"
   ```
   Установка (Windows):
   Скачать и запустить инсталлятор [rustup-init.exe](https://rustup.rs/).

2. **Git**: для клонирования репозитория.

---

## 3. Сборка на macOS

### Необходимые компоненты:
- **Xcode Command Line Tools** (для компилятора C/C++ и системных заголовков):
  ```bash
  xcode-select --install
  ```
- **Rust Toolchain**: `stable-aarch64-apple-darwin` (для Apple Silicon M1/M2/M3/M4) или `stable-x86_64-apple-darwin` (для Intel).

### Команда сборки:
```bash
cargo build --release
```
Готовый бинарник: `target/release/ag_unlocker`

### Особенности запуска на macOS:
Если система блокирует запуск («Приложение получено из неизвестного источника»):
```bash
xattr -dr com.apple.quarantine target/release/ag_unlocker
```
Для пропатчивания файлов Antigravity Терминалу может потребоваться доступ «Управление приложениями» в **Системные настройки → Конфиденциальность и безопасность**.

---

## 4. Сборка на Windows

### Необходимые компоненты:
1. **Visual Studio C++ Build Tools** (компилятор MSVC и Windows SDK):
   - Установите через [Visual Studio Installer](https://visualstudio.microsoft.com/visual-cpp-build-tools/), выбрав рабочую нагрузку: **«Desktop development with C++»** («Разработка классических приложений на C++»).
2. **Rust MSVC toolchain**: `stable-x86_64-pc-windows-msvc`.

### Команда сборки:
Откройте PowerShell или командную строку (cmd) в папке проекта:
```powershell
cargo build --release
```
Готовый бинарник: `target\release\ag_unlocker.exe`

### Запуск на Windows:
* Для полноценной работы сетевого перехватчика и автопатча запускайте **от имени администратора** (Run as Administrator).

---

## 5. Дополнительно: сборка через скрипт `build_rust.py`
В репозитории есть автоматизированный скрипт `build_rust.py`, который:
- Собирает релизные бинарники под Windows;
- При наличии WSL может выполнять кросс-сборку для Linux и macOS.

Запуск:
```bash
python3 build_rust.py
```
*(Для базовой сборки под текущую платформу достаточно стандартной команды `cargo build --release`)*.
