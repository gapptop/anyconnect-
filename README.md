https://openvpn.net/community-resources/reference-manual-for-openvpn-2-6/#encryption-options

# 准备环境

mkdir -p /etc/apt/keyrings

apt-get install gpg

curl -fsSL https://swupdate.openvpn.net/repos/repo-public.gpg | gpg --dearmor > /etc/apt/keyrings/openvpn-repo-public.gpg

echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/openvpn-repo-public.gpg] http://build.openvpn.net/debian/openvpn/testing jammy main" > /etc/apt/sources.list.d/openvpn-aptrepo.list

# 安装启动openvpn服务

wget https://raw.githubusercontent.com/Nyr/openvpn-install/master/openvpn-install.sh -O openvpn-install.sh && bash openvpn-install.sh             \# 选择udp dns 1.1.1.1那个 端口随便输别默认

echo 'mtu-disc yes' >> /etc/openvpn/server/server.conf

echo 'duplicate-cn' >> /etc/openvpn/server/server.conf

# 重启openvpn服务

sudo service openvpn restart

IPV6的DNS

2606:4700:4700::1001



# 使用IPV6连接

修改配置文件vim /etc/openvpn/server/server.conf

local <IPv4地址> #如果有私有IPV4地址需要再添加一行私有的ipv4地址，比如local 172.26.6.13

local <IPv6地址>

客户端和服务器的配置文件离得proto udp需要改为proto udp6

# 删掉自带的防火墙

可以省去很多步骤，
命令
apt remove iptables

apt autoremove
