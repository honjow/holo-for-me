# AYANEO Air Plus 适配HoloISO记录

## 安装阶段

修改HoloISO包安装脚本，设置好swap分区，构建好HoloISO包

安装到usb设备。启动系统

1. 备份内核（在内置硬盘安装的内核不包含usbhid模块，备份以备用）
2. 软连接vim为vi 执行 `cd /usr/bin; sudo ln -s vim vi`
3. 去掉vim的鼠标模式，default.vim文件位置：`/usr/share/vim/vim90/defaults.vim`，把`set mouse=a`改为`set mouse-=a`。直接执行替换命令：`sudo sed -i 's/set mouse=a/set mouse-=a/g' /usr/share/vim/vim90/defaults.vim`
4. 删除/etc/zsh/zshrc文件，执行`sudo rm /etc/zsh/zshrc`
5. 安装ohmyzsh `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
6. 设置安装ohmyzsh主题为ys, 执行`sudo sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="ys"/g' ~/.zshrc`
7. 启用zsh插件（git sudo z），执行`sudo sed -i 's/plugins=(git)/plugins=(git sudo z)/g' ~/.zshrc`
8. 编辑.zshrc文件，启用$SSH_CONNECTION判断，设置变量`export LANG=zh_CN.UTF-8`
9. 到root用户下，执行上述安装
10. 安装yay

    ``` bash
    mkdir -p ~/.honjow/git
    cd ~/.honjow/git
    sudo pacman -S --needed git base-devel
    git clone https://aur.archlinux.org/yay-bin.git
    cd yay-bin
    makepkg -si
    ```

11. 安装fcitx5

    ``` bash
    sudo pacman -S fcitx5-im fcitx5-configtool fcitx5-chinese-addons fcitx5-pinyin-zhwiki   fcitx5-material-color
    ```

12. 修改桌面屏幕方向， 文件`/etc/X11/Xsession.d/50rotate-screen`，替换`right`为`left`，执行`sudo sed -i 's/right/left/g' /etc/X11/Xsession.d/50rotate-screen`
13. 修改 gamescope-session 文件，`/usr/bin/gamescope-session`

    ``` bash
    sudo sed -i 's#-w 1280 -h 800 \\#-w 1920 -h 1080 -f \\\n\t--force-orientation left \\#;s#STEAM_DISPLAY_REFRESH_LIMITS=40,60#STEAM_DISPLAY_REFRESH_LIMITS=45,60#' /usr/bin/gamescope-session
    ```

14. 安装更纱黑体字体

    ``` bash
    yay -S ttf-sarasa-gothic
    ```

15. 设置字体优先级
    `~/.fonts.conf`

    ``` xml
    <?xml version="1.0"?>
    <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
    <fontconfig>
      <alias>
        <family>sans-serif</family>
        <prefer>
          <family>Sarasa Gothic SC</family>
          <family>Sarasa Gothic TC</family>
          <family>Sarasa Gothic J</family>
          <family>Sarasa Gothic K</family>
        </prefer>
      </alias>
      <alias>
        <family>monospace</family>
        <prefer>
          <family>Sarasa Mono SC</family>
          <family>Sarasa Mono TC</family>
          <family>Sarasa Mono J</family>
          <family>Sarasa Mono K</family>
        </prefer>
      </alias>
    </fontconfig>
    ```

16. 游戏模式下打开发者模式，打开远程调试
17. 安装decky, `curl -L http://dl.ohmydeck.net | sh`
18. 安装tomood, `curl -L http://i.ohmydeck.net | sh`