# Mac Setup

> **Updated 2026 · Apple Silicon (M-series) · macOS 14+ · Ghostty · Google Sans Code**
>
> 原本這份文件以 iTerm2 為主，現在已改用 **Ghostty**。
> 所有 Homebrew 路徑改為 Apple Silicon 的 `/opt/homebrew`（Intel Mac 請改回 `/usr/local`）。

---

## Useful Links

- Mac general: https://www.stuartellis.name/articles/mac-setup/
- Alfred + Docker settings (GUI，安裝後自行設定)

---

## 1. Homebrew

安裝 Homebrew：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

裝好後，**Apple Silicon** 需要把 Homebrew 加入 shell（寫進 `~/.zshrc`）：

```bash
eval "$(/opt/homebrew/bin/brew shellenv)"
```

確認安裝正常：

```bash
brew doctor
brew update
```

---

## 2. Git

```bash
brew install git
```

```bash
git config --global user.name "Your Name"
git config --global user.email "you@your-domain.com"
git config --global color.ui auto
```

---

## 3. Terminal：Ghostty

**不再使用 iTerm2**，改用 [Ghostty](https://ghostty.org/)。

```bash
brew install --cask ghostty
```

建立設定檔 `~/.config/ghostty/config`（完整設定也放在 [`some-setup/ghostty/config`](some-setup/ghostty/config)）：

```
# Primary font — Google Sans Code
# Symbols Nerd Font is listed second as a fallback to render powerline/p10k icons
font-family = "Google Sans Code"
font-family = "Symbols Nerd Font"
font-size = 14

# Option key behaviour: mirrors iTerm2 "Natural Text Editing"
# alt+← / alt+→ jump words; alt+backspace deletes word
macos-option-as-alt = true

# Appearance
macos-titlebar-style = tabs
copy-on-select = true
cursor-style = block

# Deepen ANSI color 4 (used by p10k path segment background)
palette = 4=#2E7D32
```

> **重點**：`font-family` 可以寫多行，Ghostty 會依順序找字符，Google Sans Code 找不到的圖示（如 p10k 箭頭）會自動 fallback 到 Symbols Nerd Font。

---

## 4. 字體

```bash
brew install --cask font-google-sans-code font-symbols-only-nerd-font
```

> ⚠️ `brew tap homebrew/cask-fonts` 已廢棄，不需要。舊的 `brew cask install` 寫法也改成 `brew install --cask`。

---

## 5. oh-my-zsh + Powerlevel10k

安裝 oh-my-zsh：

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

安裝 Powerlevel10k 主題：

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```

在 `~/.zshrc` 設定主題：

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

安裝好後，開新 terminal 會自動跑 `p10k configure` 互動設定；也可以隨時手動跑。

### 套用已儲存的設定（跳過 wizard）

如果你想直接用存好的 rainbow theme 設定，不跑互動 wizard：

```bash
curl -o ~/.p10k.zsh \
  https://raw.githubusercontent.com/PatrickSUDO/learn-note/main/some-setup/powerlevel10k/.p10k.zsh
```

然後確認 `~/.zshrc` 底部有這行（Section 10 的範例已包含）：

```zsh
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
```

重開 terminal 就直接套用，不會再跳出 wizard。

> **字型必須先裝好**（Section 4），否則 icon 會顯示成方塊。

---

## 6. zsh 外掛

### zsh-autosuggestions

自動顯示你過去輸入過的指令建議（灰色），按 `→` 或 `End` 接受。

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### zsh-syntax-highlighting

指令上色，正確的指令顯示綠色，錯誤的顯示紅色。

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

在 `.zshrc` 的 `plugins` 行啟用（**zsh-syntax-highlighting 必須放最後**）：

```bash
plugins=(git zsh-autosuggestions autojump zsh-syntax-highlighting)
```

---

## 7. 現代 CLI 工具

```bash
brew install eza fzf ripgrep fd bat navi autojump
```

| 工具 | 用途 | 取代 |
|------|------|------|
| `eza` | 好看的 ls，支援 icons / git 狀態 | 舊的 `colorls`（Ruby gem，已過時）|
| `fzf` | 模糊搜尋。`Ctrl-R` 搜歷史、`Ctrl-T` 找檔案、`Alt-C` 跳目錄 | — |
| `ripgrep` (`rg`) | 超快的 grep | `grep` |
| `fd` | 好用的 find | `find` |
| `bat` | 有語法高亮的 cat | `cat` |
| `navi` | 互動式指令備忘錄 | — |
| `autojump` (`j`) | 記錄訪問記錄，`j <目錄部分名稱>` 快速跳轉 | `cd` |

### autojump 設定

在 `~/.zshrc` 加一行：

```bash
[ -f "$(brew --prefix)/etc/profile.d/autojump.sh" ] && . "$(brew --prefix)/etc/profile.d/autojump.sh"
```

---

## 8. 語言 / 版本管理

```bash
brew install python uv node pyenv
```

- **python**：系統 Python 後援
- **uv**：現代 Python 套件 / 虛擬環境管理工具（取代 pip/virtualenv/conda）
- **node**：Node.js + npm
- **pyenv**：多版本 Python 切換

pyenv 在 `~/.zshrc` 加入：

```bash
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - zsh)"
```

---

## 9. 生產力 App

```bash
brew install --cask alfred rectangle tableplus docker visual-studio-code google-chrome
```

| App | 用途 |
|-----|------|
| Alfred | 快速啟動 / 搜尋（取代 Spotlight）|
| Rectangle | 鍵盤快速視窗排版 |
| TablePlus | 資料庫 GUI (MySQL/Postgres/SQLite 等)|
| Docker | 容器化開發環境 |
| VS Code | 程式碼編輯器 |
| Google Chrome | 開發用瀏覽器 |

---

## 10. 完整 `~/.zshrc` 範例

```zsh
# ===== Powerlevel10k instant prompt (keep near top of .zshrc) =====
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# ===== Homebrew (Apple Silicon) =====
eval "$(/opt/homebrew/bin/brew shellenv)"

# ===== PATH =====
export PATH="$HOME/.local/bin:$PATH"

# ===== pyenv =====
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - zsh)"

# ===== oh-my-zsh =====
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="powerlevel10k/powerlevel10k"
ZSH_DISABLE_COMPFIX=true
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=30'
# note: zsh-syntax-highlighting must stay last in plugins list
plugins=(git zsh-autosuggestions autojump zsh-syntax-highlighting)
source $ZSH/oh-my-zsh.sh

# ===== fzf (Ctrl-R history / Ctrl-T files / Alt-C cd) =====
source <(fzf --zsh)

# ===== autojump (j <dir>) =====
[ -f "$(brew --prefix)/etc/profile.d/autojump.sh" ] && . "$(brew --prefix)/etc/profile.d/autojump.sh"

# ===== Aliases =====
alias ls='eza --icons --group-directories-first'
alias lc='eza -lA --git --icons --group-directories-first'
alias cat='bat'
# Uncomment if you want to override system defaults:
# alias find='fd'
# alias grep='rg'

# ===== Powerlevel10k =====
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
```

---

## 常見問題修復

### zsh 啟動出現大量 warning

```bash
# 加在 ~/.zshrc
ZSH_DISABLE_COMPFIX=true
```

### alt 鍵無法刪字 / 跳字

確認 Ghostty 設定有 `macos-option-as-alt = true`（已包含在第 3 節的設定中）。
