# 1、下载并安装iterm2

```https://iterm2.com/downloads/stable/iTerm2-3_4_6.zip```

# 2、打开iterm2安装oh my zsh

执行如下脚本进行安装

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

# 3、安装powerlevel10k主题

```shell
cd ./.oh-my-zsh/themes
git clone  https://github.com/romkatv/powerlevel10k.git

或者直接
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k

vi ~/.zshrc 设置如下内容 使用p10k主题 ZSH_THEME="powerlevel10k/powerlevel10k"
```

# 4、安装语法高亮插件和自动补全插件

```
cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git


cd ~/.oh-my-zsh/custom/plugins/
git clone https://github.com/zsh-users/zsh-autosuggestions
```

下载完插件后退出iterm2
接下来 vi ~/.zshrc 在插件配置处添加下载的这两个插件名
```
plugins=(
     git
     zsh-syntax-highlighting
     zsh-autosuggestions
)
```
另外历史记录时间戳可以改成如下格式
HIST_STAMPS="yyyy-mm-dd"

# 5、p10k configure向导模式进行p10k的主题定制

定制过程中第一步提示下载字体
如果下载失败，先退出iterm2,再登录，输入代理命令后 运行p10k configure

p10k configure

再进行字体下载 然后按照wizard向导根据你喜欢的风格进行主题定制
部分截图如下
这是重新打开iterm2，体验一下定制过后的效果
例如输入过的命令自动提示，这时只需要输入方向右键就可以自动补全
界面美观且输命令也非常高效
历史记录时间戳的效果

###使用 p10k(Oh My Zsh 主题)在 Shell 中保持 Git 分支名称不被截断

```
~/.p10k.zsh配置文件内
(( $#branch > 32 )) && branch[13,-13]="…"  # <-- this line
注释调上面这句
```

# 6、iterm2 中使用Nerd Fonts字体

```
https://www.nerdfonts.com/font-downloads
```

下载字体
安装字体
iTerm2中修改为hack nerd fonts

# 7、iterm2背景图片定制
效果如下
以上就是大致的配置与美化过程，更多的美化与配置可以参考如下文章
https://cloud.tencent.com/developer/article/1639115
下面是实体机MacOS下的效果
