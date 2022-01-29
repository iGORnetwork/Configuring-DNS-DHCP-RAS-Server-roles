# Configuring-DNS-DHCP-RAS-Server-roles
## Настройка AD
### Настройка ролей и компонентов. 
1) Идём во вкладку Manage →	Add Roles and Features → выбираем role-based or feature-based installation → next → выбираем select a server from the server pool и нашь сервер DC1 → next → добавляем компоненты: active directory domain services, DHCP server, DNS server → Next
![](https://github.com/iGORnetwork/Configuring-DNS-DHCP-RAS-Server-roles/blob/main/DC1-1.png)
Вкладка Features пропускаем → next → next → next → install → clouse → перезагружаем PC .
# Настройка DHCP
Идём во вкладку Tools → DHSP → выбираем контролер домена DC1 Moscow.wsr → открываем вкладку IPv4 и правой кнопкой добовляем New Scope 
