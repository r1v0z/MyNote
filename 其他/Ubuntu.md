# Ubuntu使用

- 操作系统：Ubuntu-desktop 22.04
- 内存：4 GB
- 处理器： 4
- 网络适配器：NAT
- IP地址：192.168.224.219/24





## 1. 安装 open-vmtools

```bash
sudo apt install -y open-vm-tools open-vm-tools-desktop
reboot		# 安装完重启系统
```



## 2. 更换源

1. 先备份配置文件

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list_backup
```



2. 修改配置文件 `/etc/apt/sources.list` 的内容（用的是清华源）：

```shell
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse

# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse

deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
```



## 3. 更新系统

```bash
sudo apt update
sudo apt upgrade -y
```



## 4. 安装常用软件

- 安装常用软件

```bash
sudo apt install -y vim wget git curl
```

- 安装代理软件 `proxychains`

```bash
sudo apt install -y proxychains4
```



## 5. 安装开发者工具

```bash
#安装开发者工具
sudo apt install -y build-essential

#安装 gcc12和g++12（开发者工具中会安装11版本的gcc/g++）
sudo apt install -y gcc-12 g++-12

#管理多版本gcc/g++
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 100
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 100

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-12 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 100

#切换gcc/g++的版本
sudo update-alternatives --config gcc
sudo update-alternatives --config g++

#查看gcc/g++的版本
gcc -v
g++ -v
```



## 6.安装vscode

```bash
#下载软件包
wget https://az764295.vo.msecnd.net/stable/b3e4e68a0bc097f0ae7907b217c1119af9e03435/code_1.78.2-1683731010_amd64.deb -O vscode.deb

#安装软件
sudo dpkg -i vscode.deb
```



## 7. 安装字体

```bash
#创建存放目录
sudo mkdir /usr/share/fonts/myfonts

#将下载好的字体放到 /usr/share/fonts/myfonts 下
sudo cp -r ./consola-1.ttf /usr/share/fonts/myfonts/

#修改字体文件的权限
sudo chmod 644 /usr/share/fonts/myfonts/consola-1.ttf

#安装字体
sudo mkfontscale 
sudo mkfontdir 
sudo fc-cache -fv

#查看是否安装成功
fc-list |grep myfonts
```



## 8. zsh

### 8.1 安装 zsh

```bash
#查看是否已安装 zsh
cat /etc/shells | grep zsh

#安装 zsh
sudo apt install -y zsh

#设置当前 shell 为 zsh
chsh -s /bin/zsh

#重启系统
sudo reboot
```

### 8.2 安装 zim

```bash
wget -nv -O - https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
```

### 8.3 安装  Powerlevel10k

```bash
#在配置文件中添加一行
zmodule romkatv/powerlevel10k

#安装
zimfw install

#重新打开终端，可以输入 q 退出配置

#重新进行配置
p10k configure
```



### 8.4 下载字体库

```bash
#下载字体库
git clone https://github.com/ryanoasis/nerd-fonts.git --depth 1

#安装
cd nerd-fonts 
./install.sh

#根据个人情况看是否删除
cd ..
rm -rf nerd-fonts

#修改终端字体为 Hack Nerd Font
```



### 8.5 报错

```bash
[ERROR]: When using Powerlevel10k with instant prompt, prompt_cr must be unset.

#出现以上的报错，在~/.zshrc 中添加 unsetopt PROMPT_CR
```



## 9. 主题更换

### 9.1主题

```bash
sudo apt install gnome-tweaks

# 打开 Firefox 安装插件
https://extensions.gnome.org/

sudo apt install chrome-gnome-shell
sudo apt install gnome-themes-extra gtk2-engines-murrine sassc


#下载
https://github.com/vinceliuice/Orchis-theme/releases

#安装
./install.sh -c dark -t all -l
```



### 9.2 图标

```bash
#下载
https://github.com/vinceliuice/Tela-icon-theme/releases

#安装
./install.sh -a
```

