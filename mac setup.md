# Mac Setup

## Useful Link

Mac general

- https://www.stuartellis.name/articles/mac-setup/

Iterm2 + zsh

- https://juejin.cn/post/6844904178075058189 
- https://medium.com/%E6%95%B8%E6%93%9A%E4%B8%8D%E6%AD%A2-not-only-data/macos-%E7%9A%84-terminal-%E5%A4%A7%E6%94%B9%E9%80%A0-iterms-oh-my-zsh-%E5%85%A8%E6%94%BB%E7%95%A5-77d5aae87b10





```
# Powerlevel9k icon 顯示
POWERLEVEL9K_MODE='nerdfont-complete'
# Powerlevel9k command line 左邊想顯示的內容
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(virtualenv dir dir_writable vcs) 
# Powerlevel9k command line 右邊想顯示的內容
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status ram)
```







## Terminal setup (oh-my-zsh + iterms)



```bash
brew install iterm2
```



```bash
brew install zsh
```



install oh my zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```





在安裝 Oh-my-zsh 後他會問你是否要默認 zsh 為預設 shell，大大方方的按下 y + enter，就正式進入 Oh-my-zsh 的世界啦！

如果當初忘記轉換的玩家，可以在安裝完後輸入下列指令轉換。



```bash
sudo sh -c "echo $(which zsh) >> /etc/shells"
chsh -s $(which zsh)
```



- 用 `Homebrew` 安裝的 `Zsh` 位置在 `/usr/local/bin/zsh`，而系統安裝的則會在` /bin/zsh`。



#### 安装字体

你可以如官网所说，通过 `brew` 来安装：

```bash
brew tap homebrew/cask-fonts
brew cask install font-hack-nerd-font
```

#### zshrc 设置字体

```bash
POWERLEVEL9K_MODE="nerdfont-complete"
ZSH_THEME="powerlevel10k/powerlevel10k"复制代码
```

注意，需要设置在 `ZSH_THEME` 之前。

#### iTerm2 设置字体

操作路径：菜单栏 -> Profiles -> Open Profiles -> Edit Profiles -> 选择 Text

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/1/1726f38f0a297b08~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

这样，所有的图标就都可以正常显示了。

## colors

这是一个文件目录美化插件，如图所示：

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/1/172700257e52ae07~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

```bash
gem install colorls
```

然后执行 `colors` 就好了，你也可以设置 `alias` 更高效一点：

```bash
alias lc='colorls -lA --sd'
```

设置了别名之后，就像我一样，输入 `lc` 就好了。

我就只用了以上几个插件，已经能够大幅度提升工作效率了，如果有其它好用的插件，一定要告诉我呀。

## Zsh-autosuggestions

能夠自動幫你把過去輸入過的資訊提示出來，真的真的真的省了很多輸入的時間啊啊啊～大推這個套件，用過後就回不去了xD

[zsh-users/zsh-autosuggestionsFish-like autosuggestions for zsh. Contribute to zsh-users/zsh-autosuggestions development by creating an account on…github.com](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md)

```bash
# 下載套件至 Zsh 的 plugin 裡
$ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions# 啟用套件（在 ~/.zshrc 裡）
plugins=(zsh-autosuggestions)
```

如果對於預設的提示字體顏色覺得太深，可以到下列位置修改：

> ```
> ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
> ```

**調整顯示顏色：**

```bash
# 替換調 fg=8 換成其他顏色
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=8'
```

`fg=8` 的數字是 0 ~ 255，或者直接填寫常用的 8 種顏色文字 `black, red, green, yellow, blue, magenta, cyan and white` 我自己是習慣使用 `fg=30`的色票，不會太搶眼卻又不至於看不到文字。



```bash
＃If not working 
source .oh-my-zsh/custom/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
```



## zsh-syntax-highlighting

不同的指令會自動幫你上色，讓你知道自己是不是輸入正確的指令。

```bash
# 下載套件
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting# 啟用套件
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```



```bash
#if not working 
source .oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```





## Naviexport EDITOR="nvim"

命令行記錄套件，能夠一站式的紀錄所有過去的指令，還有內建一堆已經建立好的快捷！

[命令行忘性大？这个开源备忘工具一次解决你的所有烦恼实名推荐这个小工具，交互式的命令行备忘录，简直解决了我们记不住命令的烦恼。 命令行是非常高效的工具，但一个很常见的现象是，很多命令行过一段时间就容易忘。举个栗子，如果我们常用 git 命令行管理代码、利用 conda…zhuanlan.zhihu.com](https://zhuanlan.zhihu.com/p/83584149)

安裝指令：

```bash
brew install navi
```

## autojump 插件

`autojump` 插件会记录你所有的访问记录，不同单独配置，直接访问即可。

### 安装

```bash
brew install autojump
复制代码
```

##### 配置

打开 `~/.zshrc` 加一行代码：

```bash
[[ -s $(brew --prefix)/etc/profile.d/autojump.sh ]] && . $(brew --prefix)/etc/profile.d/autojump.sh
复制代码
```

然后就是 `source` 一下就生效了。

##### 使用

使用 `j` 命令就可以执行 `auto-jump`，比如 `j articles`：

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/6/1/1727002559305cd1~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)

前提是你访问过 `articles` 目录，也就是你得让它记住。



