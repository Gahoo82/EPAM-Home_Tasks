## Linux Networking
### Task
Практична частина модуля Linux Networking  передбачає створення засобами Virtual Box мережі, що показаний на рисунку 1
<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/NetworkTasc.Pic_1.png">
</p>
  
__Host__ – це комп’ютер, на якому запущений Virtual Box;

__Server_1__ – Віртуальна машина, на якій розгорнуто ОС Linux. Int1 цієї машини в режимі «Мережевий міст» підключений до мережі Net1, тобто знаходиться в адресному просторі домашньої мережі. IP-адреса Int1 встановлюється статично відповідно до адресного простору, наприклад 192.168.1.200/24. Інтерфейси Int2 та Int3 відповідно підключено в режимі «Внутрішня мережа» до мереж Net2 та Net3. 

__Client_1 та Client_2__ – Віртуальні машини, на яких розгорнуто ОС Linux (бажано різні дистрибутиви, наприклад Ubuntu та CentOS). Інтерфейси підключені в режимі «Внутрішня мережа» до мереж Net2, Net3 та Net4 як показано на рисунку 1. 

Адреса мережі Net2 – 10.Y.D.0/24, де Y – дві останні цифри з вашого року народження, D – дата народження.   
Адреса мережі Net3 – 10.M.Y.0/24, де M – номер місяця народження. \
Адреса мережі Net4 – 172.16.D.0/24.

__Увага!__ Якщо, адресний простір Net2, Net3 або Net4 перетинається з адресним 
простором Net1 – відповідну адресу можна змінити на власний розсуд. 
1. На Server_1 налаштувати статичні адреси на всіх інтерфейсах. 
2. На Server_1 налаштувати DHCP сервіс, який буде конфігурувати адреси Int1, Client_1 та Client_2 
3. За допомогою команд ping та traceroute перевірити зв'язок між віртуальними машинами. Результат пояснити. \
__Увага!__ Для того, щоб з Client_1 та Client_2 проходили пакети в мережу Internet (точніше щоб повертались з Internet на Client_1 та Client_2) на Wi-Fi Router необхідно налаштувати статичні маршрути для мереж Net2 та Net3. Якщо такої можливості немає інтерфейс Int1 на Server_1 перевести в режим NAT. 
4. На віртуальному інтерфейсу lo Client_1 призначити дві ІР адреси за таким правилом: 172.17.D+10.1/24 та 172.17.D+20.1/24. Налаштувати маршрутизацію таким чином, щоб трафік з Client_2 до 172.17.D+10.1 проходив через Server_1, а до 172.17.D+20.1 через Net4. Для перевірки використати traceroute. 
5. Розрахувати спільну адресу та маску (summarizing) адрес 172.17.D+10.1 та 172.17.D+20.1, при чому префікс має бути максимально можливим. Видалити маршрути, встановлені на попередньому кроці та замінити їх об’єднаним маршрутом, якій має проходити через Server_1. 
6. Налаштувати SSH сервіс таким чином, щоб Client_1 та Client_2 могли підключатись до Server_1 та один до одного.  
7. Налаштуйте на Server_1 firewall таким чином:
- Дозволено підключатись через SSH з Client_1 та заборонено з Client_2 
- З Client_2 на 172.17.D+10.1 ping проходив, а на 172.17.D+20.1 не проходив 
8. Якщо в п.3 була налаштована маршрутизація для доступу Client_1 та Client_2 до мережі Інтернет – видалити відповідні записи. На Server_1 налаштувати NAT 
сервіс таким чином, щоб з Client_1 та Client_2 проходив ping в мережу Інтернет.

### Networks data
__Server_1__ 
- Int1: 192.168.0.100/24. 

__Client_1 та Client_2__ \
Адреса мережі Net2 – 10.Y.D.0/24, де Y(82) – дві останні цифри з вашого року народження, D(29) – дата народження. \
Адреса мережі Net3 – 10.M.Y.0/24, де M(10) – номер місяця народження. \
Адреса мережі Net4 – 172.16.D.0/24

 - Net2: 10.82.29.0/24  
 - Net3: 10.10.82.0/24
 - Net4: 172.16.29.0/24
 
<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/network_linux/Networks_using_Linux/Docs/Table%20network.png">
</p>

#### 1. На Server_1 налаштувати статичні адреси на всіх інтерфейсах.
Приховуємо файл дефолтних налаштувань шляхом зміни назви та створюємо новий файл налаштувань
```console
kostia@Server1:/etc/netplan$ ls -l
total 8
-rw-r--r-- 1 root root 117 Dec  6 17:57 00-installer-config.yaml.org
-rw-r--r-- 1 root root 432 Dec 19 21:37 server1-config.yaml
kostia@Server1:/etc/netplan$ sudo nano server1-config.yaml
```
Конфігуруємо файл мережевих налаштувань "server1-config.yaml"

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/1_Static_IP_all_interfaces_netplan.png">
</p>

#### 2. На Server_1 налаштувати DHCP сервіс, який буде конфігурувати адреси Int1, Client_1 та Client_2
Налаштовуємо файл "isc-dhcp-server"
```console
sudo nano /etc/default/isc-dhcp-server

INTERFACESv4="enp0s8 enp0s9"
```
<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/isc_dhcp_server.png">
</p>

Налаштовуємо файл "dhcp.conf"
```console
sudo nano /etc/dhcp/dhcpd.conf
```
<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/dhcp.conf.png">
</p>

Перезавантажуємо DHCP-server та systemd-networkd (systemd-networkd також в подальшому для Client1/Client2), перевіряємо IP-адресу
```console
sudo service isc-dhcp-server restart
# OR
sudo systemctl restart isc-dhcp-server.service
```
```console
sudo systemctl status isc-dhcp-server
```
```console
sudo systemctl restart systemd-networkd
ip addr 
```
<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/Server1_IP_addr.png">
</p>

#### Налаштовуємо мережеві інтерфейси на Client1
Конфігуруємо файл мережевих налаштувань у папці Netplan. 
Int1-enp0s3 налаштовуємо на отримання IP-адреси від DHCP-серверу Server1.
На Int2-enp0s8 налаштовуємо статичну IP-адресу(172.16.29.1) відповідно до мережі 172.16.29.0

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/Client1_netplan1.png">
</p>

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/Client1_IP_addr.png">
</p>

#### Налаштовуємо мережеві інтерфейси на Client2.
Редагуємо конфігураційні файли "ifcfg-enp0s3" та "ifcfg-enp0s8" для відповідних інтерфейсів. Так щоб enp0s3 отримував IP-адресу від DHCP-серверу Server1. А на enp0s8 налаштовуємо статичну адресу 172.16.29.2 
Після цього перезапускаємо network

```console
sudo systemctl restart network
```
<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/Client2_dhcp%26static_ip.png">
</p>

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/Client2_ip_addr.png">
</p>

3. За допомогою команд ping та traceroute перевіряємо зв'язок між віртуальними машинами. 
Налаштовуємо статичну маршрутизацію на роутері для мереж Net2 та Net3. 

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/4_ping_traceroute.png">
</p>

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/Traceroute_8888.png">
</p>

#### 4. На віртуальному інтерфейсу lo Client_1 призначити дві ІР адреси за таким правилом: 172.17.D+10.1/24 та 172.17.D+20.1/24. Налаштувати маршрутизацію таким чином, щоб трафік з Client_2 до 172.17.D+10.1 проходив через Server_1, а до 172.17.D+20.1 через Net4. Для перевірки використати traceroute. 

Таким чином маємо такі адреси: 
172.17.39.1/24
172.17.49.1/24

Для тимчасового налаштування адрес на lo інтерфейсі можемо використати команди:
```console
sudo ip address add 172.17.39.1/24 dev lo
sudo ip address add 172.17.49.1/24 dev lo
```
Для Netplan:
```console
network:
    version: 2
    renderer: networkd
    ethernets:
        lo:
            addresses: [172.17.39.1/24, 172.17.49.1/24]
```
Конфігуруємо маршрутизацію для Client1, Server1, Client2

<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/lo_interface.png">
</p>

Додаємо правила для транзиту пакетів на Server1
```console
sudo iptables -A FORWARD -i enp0s8 -o enp0s9 -j ACCEPT
sudo iptables -A FORWARD -i enp0s9 -o enp0s8 -j ACCEPT

# Save current rules:
sudo iptables-save

sudo sh -c "iptables-save > /etc/iptables/rules.v4"
```
<p align="center">
  <img src="https://github.com/Gahoo82/EPAM-Home_Tasks/blob/main/Networks_using_Linux/Docs/IP_table_Server_for_lo.png">
</p>
