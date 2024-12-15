https://wiki.debian.org/wl
下载3个包备用
https://packages.debian.org/bookworm/lsb-release
https://packages.debian.org/bookworm/dkms
https://packages.debian.org/bookworm/broadcom-sta-dkms

sudo su
# dpkg -i *.deb
modprobe -r b44 b43 b43legacy ssb brcmsmac bcma
modprobe wl
# 连接wifi, 修改连接，设置静态ip

# 添加必备软件
sed -i 's/deb.debian.org/mirrors.ustc.eud.cn/g' /etc/apt/sources.list
apt update && apt upgrade
apt --purge remove ibus
apt install fcitx5 wget openssh-server xrdp pipewire-pulse pipewire-alsa pipewire-module-xrdp
apt autoremove
rm -rf /usr/share/ibus

# ssh允许空密码登陆
sed -i 's/#PermitEmptyPasswords no/PermitEmptyPasswords yes/' /etc/ssh/sshd_config
systemctl restart ssh

# 准备用rdp连接，把会话管理干掉
mv /usr/sbin/lightdm /usr/sbin/lightdm.bak

reboot