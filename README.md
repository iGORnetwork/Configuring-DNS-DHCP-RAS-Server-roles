# Configuring-DNS-DHCP-RAS-Server-roles
## Настройка DC1 AD
### Настройка ролей и компонентов. 
1) Идём в AD во вкладку Manage →	Add Roles and Features → выбираем role-based or feature-based installation → next → выбираем select a server from the server pool и нашь сервер DC1 → next → добавляем компоненты: active directory domain services, DHCP server, DNS server → Next
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-1.png)
Вкладка Features пропускаем → next → next → next → install → clouse → перезагружаем PC .
# Контроллер домена 
1)В правом верхнем углу кликаем на флажок и выбираем параметр → promote this server to a domain controller.
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-4.png)
2) Создаем новый лес → add new forest → name Moscow.wsr → next → ставим пароль → next → next → next → install → clouse 
# DHCP
1) Идём в AD во вкладку Tools → DHSP → выбираем контролер домена DC1 Moscow.wsr → открываем вкладку IPv4 и правой кнопкой добовляем New Scope 
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-2.png)
Next → води name LAN1 → next → водим не занятый диапазон адресов 172.16.19.70 : 172.16.19.120 → указываем маску 255.255.255.192 → next → next →
Router default gateway водим шлюз 172.16.19.126 → add → next → domain name server dns добовляем name Moscow.wsr и IP 172.16.19.65 → add → next → next → next → finish.
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-3.png)
# DNS записи типа A и PTR 
1) Идём в AD во вкладку Tools → DNS → DC1 → forward lookup zones → Moscow.wsr → добовляем New Host 
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-5.png)
2) Водим Name CLI1 → IP adress 172.16.19.70 → отмечаем create associated pointer ptr record → add host.
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-6.png)
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-7.png)
3) Создаем зону обратного просмотра, идём во вкладку Reverse lookup zone → new zone. 
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-8.png)
Primary zone → next → DNS domain Moscow.wsr → next → network ID 172.16.19 → next → finish
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-9.png)
# Элементы доменной инфраструктуры
1) Идём в AD во вкладку Manage → active directory users and computers → выбираем домен Moscow.wsr → new → organization unit 
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-10.png)
Добовляем две новые группы IT и SALE , Name → cancel
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-11.png)
2) добавим нового пользовался → active directory users and computers → выбираем контейнер IT → new → User → Name Vasy → password → finih.
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-%2012.png)
# Настройка AD SRV1
1) Устанавливаем AD → CMD → Powershell → Install-WindowsFeature -Name AD-Domain-Services
2) Водим SRV1 в домен → CMD → Powershell → водим в одну строчку add-computer -domainname moscow.wsr водим пользователя и пароль, презагружаем SRV1
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/SRV1-1.png)
3) Возвращаемся DC1 AD идём во вкладку manage → add server → вкладка DNS и добавляем PC SRV1 и нажимаем ОК.
4) На странице быстрого доступа AD выбираем вкладка All server и выбираем наш резервный сервер SRV1.
5) Далее правой кнопкой на SRV1 выбираем  Add Roles and Features и добавляем компоненты по аналогии с DC 1 → DHCP , DNS.
6) В правом верхнем углу кликаем на флажок и Применяем наши настройки.
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-14.png)
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-13.png)
7) Сделаем SRV1 дополнительным контролером домена 
Server Manager → tools → Active directory sites and services.
Разверните вкладку Sites → Default-First-Site-Name → Servers → SRV1 → NTDS Settings
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-15.png)
Щелкните правой кнопкой мыши по элементу automatically generated → Replicate now 
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-16.png)
Повторим то же самое DC1
# Настройка AD DCA
1) Водим DCA в домен WIN+r → CMD → Powershell → водим в одну строчку add-computer -domainname moscow.wsr водим пользователя и пароль, презагружаем DCA
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DCA-1.png)
# Настройка AD CLI1 
1) Водим CLI1 в домен WIN+r → CMD → Powershell → водим в одну строчку add-computer -domainname moscow.wsr водим пользователя и пароль, презагружаем CLI1
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/CLI1-1.png)
# Настройка AD DC2
Дольнейшаа настройка проводиться аналогично первой , Name контролера домена spb.wsr и настройки сети для ip 172.16.20.96/27
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC2-1.png)
# Настройка AD SRV2
настройка проводиться аналогично SRV1
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC2-2.png)
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC2-3.png)
# Настройка AD CLI2 
настройка проводиться аналогично CLI1
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/CLI2-1.png)
