# Configuring-DNS-DHCP-RAS-Server-roles
## Настройка AD
### Настройка ролей и компонентов. 
1) Идём во вкладку Manage →	Add Roles and Features → выбираем role-based or feature-based installation → next → выбираем select a server from the server pool и нашь сервер DC1 → next → добавляем компоненты: active directory domain services, DHCP server, DNS server → Next
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-1.png)
Вкладка Features пропускаем → next → next → next → install → clouse → перезагружаем PC .
# Контроллер домена 
1)В правом верхнем углу кликаем на флажок и выбираем параметр → promote this server to a domain controller.
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-4.png)
2) Создаем новый лес → add new forest → name Moscow.wsr → next → ставим пароль → next → next → next → install → clouse 
# DHCP
1) Идём во вкладку Tools → DHSP → выбираем контролер домена DC1 Moscow.wsr → открываем вкладку IPv4 и правой кнопкой добовляем New Scope 
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-2.png)
Next → води name LAN1 → next → водим не занятый диапазон адресов 172.16.19.70 : 172.16.19.120 → указываем маску 255.255.255.192 → next → next →
Router default gateway водим шлюз 172.16.19.126 → add → next → domain name server dns добовляем name Moscow.wsr и IP 172.16.19.65 → add → next → next → next → finish.
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-3.png)
# DNS 
1) Идём во вкладку Tools → DNS → DC1 → forward lookup zones → Moscow.wsr → добовляем New Host 
