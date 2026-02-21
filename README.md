🚀 Zapret-Gateway: Свободный интернет на старом железе / Free Internet on Old Hardware
🇷🇺 Русская версия
Этот гайд поможет вам превратить старый компьютер в прозрачный сетевой шлюз, который восстановит нормальную работу YouTube (включая 4K на ТВ) и других ресурсов для всех устройств в доме без необходимости устанавливать софт на каждый гаджет.

🛠 Железо
Сервер: Любой старый ПК (в моем случае — Intel Pentium G630 / 8 GB RAM / БП 450W).

ОС: Linux (Debian или Ubuntu).

Клиенты: Все устройства в домашней сети (Smart TV, смартфоны, консоли, ПК).

📥 1. Установка и настройка
Обновите систему: sudo apt update && sudo apt upgrade -y

Установите Zapret:

git clone https://github.com/bol-van/zapret.git

cd zapret

sudo ./install_easy.sh

При установке выбирайте движок nfqws и списки antizapret.

⚙️ 2. Оптимальный конфиг (Файл /opt/zapret/config)
Для обхода блокировок на уровне провайдера (проверено на ЕОС) используйте эти параметры в секции NFQWS_OPT:

NFQWS_OPT="
--filter-tcp=80 --dpi-desync=split --dpi-desync-ttl=0 <HOSTLIST> --new
--filter-tcp=443 --dpi-desync=fake,disorder --dpi-desync-split-pos=1 --dpi-desync-ttl=5 <HOSTLIST> --new
--filter-udp=443 --dpi-desync=fake --dpi-desync-repeats=6 <HOSTLIST>
"
🌐 3. Настройка сети (Шлюз)
Чтобы сервер пропускал через себя трафик, включите пересылку пакетов:

echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
Как подключить устройства:

Вариант А (DHCP): В настройках роутера укажите IP сервера как Default Gateway (Опция DHCP 3).

Вариант Б (Ручной): В настройках Wi-Fi на ТВ или телефоне укажите IP сервера в поле «Шлюз».

🇺🇸 English Version
This guide will help you transform an old PC into a transparent network gateway that restores normal YouTube performance (including 4K on TV) and bypasses DPI for all devices in your home network.

🛠 Hardware
Server: Any old PC (e.g., Intel Pentium G630 / 8 GB RAM).

OS: Linux (Debian or Ubuntu).

Clients: All home devices (Smart TV, smartphones, PCs).

📥 1. Installation
Update your system: sudo apt update && sudo apt upgrade -y

Install Zapret:

git clone https://github.com/bol-van/zapret.git
cd zapret
sudo ./install_easy.sh
Choose nfqws engine and antizapret lists during setup.

⚙️ 2. Optimal Configuration (File /opt/zapret/config)
Use these parameters in the NFQWS_OPT section for effective DPI circumvention:

NFQWS_OPT="
--filter-tcp=80 --dpi-desync=split --dpi-desync-ttl=0 <HOSTLIST> --new
--filter-tcp=443 --dpi-desync=fake,disorder --dpi-desync-split-pos=1 --dpi-desync-ttl=5 <HOSTLIST> --new
--filter-udp=443 --dpi-desync=fake --dpi-desync-repeats=6 <HOSTLIST>
"
🌐 3. Network Routing (Gateway Mode)
Enable IP forwarding to allow the server to act as a gateway:

echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
Connecting Devices:

Option A (DHCP): Set the server's IP as the Default Gateway in your router's DHCP settings.

Option B (Manual): Manually set the server's IP as the "Gateway" in the Wi-Fi settings of your TV or phone.

Author: nudivi
