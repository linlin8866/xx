# sinbox 一键脚本

## 一键安装（推荐）
```bash
bash <(curl -L https://raw.githubusercontent.com/linlin8866/xx/main/sinbox.sh)
备用安装方式
wget -O - https://raw.githubusercontent.com/linlin8866/xx/main/sinbox.sh | bash
一键命令
bash <(curl -L https://raw.githubusercontent.com/linlin8866/xx/main/sinbox.sh)
bbr一键命令
# 一键安装魔改BBR（选一个即可）
# BBRplus
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
# BBRv2
wget -N --no-check-certificate "https://raw.githubusercontent.com/google/bbr/master/v2/setup.sh" && chmod +x setup.sh && ./setup.sh


bbr一键命令
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

验证bbr
sysctl net.ipv4.tcp_congestion_control
lsmod | grep bbr
如果恢复
wget -N --no-check-certificate "https://github.com/ylx2016/Linux-NetSpeed/raw/master/BBR2/bbr2.sh" && chmod +x bbr2.sh && ./bbr2.sh
openwrt安装bbr
# 切回默认
sysctl -w net.ipv4.tcp_congestion_control=cubic
# 卸载模块
rmmod tcp_bbr
# 卸载ipk包
opkg remove kmod-tcp-bbr
# 清理配置
sed -i '/bbr/d' /etc/sysctl.conf
sysctl -p

openwrt安装bbr
# 安装魔改BBR模块（需对应内核版本）
opkg update
opkg install kmod-tcp-bbr_mod
# 加载模块
insmod tcp_bbr_mod
# 设置默认
echo "net.ipv4.tcp_congestion_control=tcp_bbr_mod" >> /etc/sysctl.conf
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
sysctl -p

验证
sysctl net.ipv4.tcp_congestion_control  # 应显示tcp_bbr_mod
lsmod | grep bbr_mod
