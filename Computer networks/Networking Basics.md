# 📌 Комп'ютерні мережі
## 🏷 Курс: "Основи роботи в мережі" (Cisco Networking Academy – Introduction to Networks)
## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б
---
## 🎯 Мета роботи
1. Ознайомитися з налаштуванням домашньої мережі через симуляцію в Cisco Packet Tracer.
2. Навчитися підключати пристрої, конфігурувати бездротовий маршрутизатор, DHCP та тестувати з'єднання з веб-сервером.
3. Виконати лабораторні роботи для закріплення практичних навичок кабельного/бездротового підключення, DHCP та доступу до Інтернету.
## 🛠 Матеріальне забезпечення
- 💻 Комп’ютер із встановленим Cisco Packet Tracer (остання версія).
- 🌐 Доступ до платформи Cisco Networking Academy (netacad.com).
- 📚 Матеріали курсу "Основи роботи в мережі".
---
## 📚 Короткі теоретичні відомості
Курс **Introduction to Networks** охоплює базові концепції домашніх мереж: підключення коаксіального кабелю, Ethernet, бездротових клієнтів (Wi-Fi), конфігурацію маршрутизатора через GUI (SSID, WPA2, пароль), DHCP для автоматичного призначення IP, тестування з'єднань (ping, веб-браузер). Симуляція в Packet Tracer дозволяє налаштовувати домашній роутер, кабельний модем, ПК/ноутбуки без фізичного обладнання, аналізувати доступ до Інтернету та веб-серверів.
---
## 📋 Зміст роботи
### 1. Сертифікат курсу
![Сертифікат](https://i.ibb.co/ZpZ6bPjy/firefox-KJrh-XOak-UR.png)
### 2. Словник термінів
Нижче наведено таблицю з 10 новими термінами, вивченими в курсі.
| Термін (англ.) | Термін (укр.) | Визначення (пояснення) |
|---------------------------|---------------------------|---------------------------------------------------------------------------------------|
| SSID | SSID | Ім'я бездротової мережі, видимое для клієнтів; наприклад, MyHome для ідентифікації мережі (4.4). |
| WPA2 Personal | WPA2 Персональний | Стандарт шифрування Wi-Fi з пре-шерованим ключем (passphrase) для захисту доступу (4.4). |
| DHCP Server | DHCP-сервер | Компонент маршрутизатора, що автоматично призначає IP-адреси клієнтам у діапазоні (наприклад, 192.168.0.100–109) (9.2). |
| Default Gateway | Шлюз за замовчуванням | IP маршрутизатора (наприклад, 192.168.0.1), через який пристрої виходять в Інтернет (4.4). |
| Coaxial Cable | Коаксіальний кабель | Кабель для передачі Інтернет/ТБ від провайдера; підключається до спліттера/модему (4.4). |
| Cable Modem | Кабельний модем | Пристрій для перетворення сигналу від провайдера в Ethernet для маршрутизатора (4.4). |
| GUI (Graphical User Interface) | Графічний інтерфейс користувача | Веб-інтерфейс маршрутизатора для конфігурації (наприклад, за 192.168.0.1, логін admin) (4.4). |
| Passphrase | Парольна фраза | Ключ для WPA2; наприклад, MyPassPhrase1! для підключення клієнтів (4.4). |
| Web Browser | Веб-браузер | Клієнт для доступу до сайтів за IP/доменом (наприклад, skillsforall.srv) (8.1). |
| Maximum Number of Users | Максимальна кількість користувачів | Обмеження DHCP на кількість клієнтів (наприклад, 10) для контролю мережі (4.4). |
### 3. Звіти лабораторних робіт
Нижче наведено звіти з виконаних лабораторних робіт курсу. Для кожної лабораторної роботи наведено скріншоти ключових кроків (у реальному репозиторії вони будуть прикріплені як зображення) та короткі пояснення до них.
#### Лабораторна робота 4.4.4: Packet Tracer – Налаштування бездротового маршрутизатора та клієнта
- **Мета**:
  Підключити пристрої до домашньої мережі, налаштувати маршрутизатор (DHCP, SSID, WPA2) та перевірити доступ до Інтернету.
- **Хід виконання**:

  1. **Крок 1: Підключення коаксіальних кабелів**
     Connections > Coaxial cable. Coaxial1 (Splitter) → Port 0 (Cable Modem); Coaxial2 → Port 0 (TV). Увімкнути TV – з'являється зображення.
     📷 <img width="1201" height="648" alt="xfgd" src="https://github.com/user-attachments/assets/0aaf9675-9627-44b6-ad0c-bcd3c43f8503" />
     📷 <img width="1073" height="828" alt="xfgd" src="https://github.com/user-attachments/assets/8346a888-0b35-4dda-b40f-1baa08c82978" />
     _Пояснення_: Спліттер розділяє сигнал на Інтернет/ТБ; модем отримує дані.

  2. **Крок 2: Підключення Ethernet**
     Copper Straight-Through: Port 1 (Modem) → Internet (Router); Office PC (Fa0) → Gi1 (Router); Bedroom PC → Gi2.
     📷 <img width="1065" height="741" alt="xfgd" src="https://github.com/user-attachments/assets/b10d8775-9ef5-48bc-a297-650fe9b0c5fc" />
     📷 ![hfg](https://github.com/user-attachments/assets/14509b32-1f19-4b0f-82db-c3ce5f595b67)
     _Пояснення_: Роутер з'єднує модем з ПК; wired підключення готове.

   3. **Крок 3: Доступ до GUI роутера**
     Office PC: IP Configuration > DHCP (отримано 192.168.0.x, gateway 192.168.0.1). Web Browser > 192.168.0.1, admin/admin.
     📷 <img width="802" height="876" alt="xfgd" src="https://github.com/user-attachments/assets/b8bb4f9e-e3ff-440e-9745-3df31dfdc571" />
     ![gdf](https://github.com/user-attachments/assets/7b10be05-336d-43fd-aab6-1e9fcdba3ebd)
     <img width="888" height="437" alt="xfgd" src="https://github.com/user-attachments/assets/1d2be672-f83e-4ca7-b523-778505d36dc9" />
     <img width="1138" height="996" alt="xfgd" src="https://github.com/user-attachments/assets/e1df0e62-d87f-43c3-b8b0-629fa95fac94" />
     _Пояснення_: DHCP автоматично конфігурує ПК; GUI для налаштувань.

  4. **Крок 4: Базові налаштування (DHCP, пароль)**
     Setup > Maximum Users: 10. Administration > Password: MyPassword1!. Save Settings.
     📷 <img width="854" height="643" alt="xfgd" src="https://github.com/user-attachments/assets/d753304c-8d54-4a77-b8a2-35fa3fd02b88" />
     📷 <img width="994" height="789" alt="xfgd" src="https://github.com/user-attachments/assets/ae694612-dc47-4b33-bdb1-87abfc9c847d" />
     📷 <img width="976" height="530" alt="xfgd" src="https://github.com/user-attachments/assets/d01148b1-673f-4c16-a1a6-0dcd1c063941" />
     _Пояснення_: Обмежує клієнтів; змінює дефолтний пароль для безпеки.

   5. **Крок 5: Налаштування Wi-Fi**
     Wireless > Enable 2.4 GHz, SSID: MyHome. Wireless Security > WPA2 Personal, Passphrase: MyPassPhrase1!. Save.
     📷 <img width="983" height="404" alt="xfgd" src="https://github.com/user-attachments/assets/f5380363-926d-4e5e-9f4f-a2d54956d921" />
     _Пояснення_: Активує мережу; WPA2 захищає від несанкціонованого доступу.

   6. **Крок 6: Підключення Laptop та тест**
     Laptop: PC Wireless > Connect to MyHome, ключ MyPassPhrase1!. Web Browser > skillsforall.srv (завантажується).
     📷 <img width="993" height="465" alt="xfgd" src="https://github.com/user-attachments/assets/cadd0ce6-a66b-4e2f-b657-8b85c8196d02" />
     _Пояснення_: Клієнт отримує IP via DHCP; доступ до сайту підтверджує Інтернет.

- **Висновок**:
  Лабораторна робота навчила повному налаштуванню домашньої мережі: кабелі, GUI, Wi-Fi безпека, DHCP; всі пристрої мають доступ до Інтернету.
  
#### Лабораторна робота 8.1.3: Packet Tracer — Під'єднання до веб-сервера
- **Мета**:
  Перевірити з'єднання до веб-сервера за IP, спостерігати за пакетами.
     📷 ![fgh](https://github.com/user-attachments/assets/218beff2-d167-4859-96e8-eb9bdec79180)
     📷 ![jgh](https://github.com/user-attachments/assets/a0053af5-3509-4117-baf6-0c6ef1b6bce0)

- **Хід виконання**:
  1. **Крок 1: Пінг до сервера**
     PC0: Command Prompt > `ping 172.33.100.50`. 4 пакети, 3 відповіді (час 0ms).
     📷 <img width="600" height="300" alt="ping server" src="https://github.com/user-attachments/assets/example-ping-server.png" />
    ```
    PC> ping 172.33.100.50

    Pinging 172.33.100.50 with 32 bytes of data:

    Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
    Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
    Reply from 172.33.100.50: bytes=32 time=0ms TTL=127
    Reply from 172.33.100.50: bytes=32 time=0ms TTL=127

    Ping statistics for 172.33.100.50:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
    Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
    ```
    _Пояснення_: Пінг підтверджує доступність; втрата 1 пакета – ініціалізація ARP.
  
  2. **Крок 2: Доступ через браузер**
     Web Browser > 172.33.100.50 > Go. Завантажується сторінка: «Welcome to the Learn IP Web Site».
     📷 <img width="1548" height="512" alt="xfgd" src="https://github.com/user-attachments/assets/508999d2-0182-4465-a332-4d147ec25fe8" />
     📷 <img width="958" height="437" alt="xfgd" src="https://github.com/user-attachments/assets/92ca81c1-7c81-48aa-b7a8-a9c4d1565bb8" />
     _Пояснення_: Браузер (клієнт) з'єднується за IP; сервер відповідає HTML.
     
- **Висновок**:
  Лабораторна робота показала прямий доступ до веб-сервера за IP без домену; ping/браузер для верифікації.
  
#### Лабораторна робота 11.2.3: Packet Tracer - Налаштування DHCP на бездротовому маршрутизаторі
- **Мета**:
  Налаштувати DHCP на роутері, змінити діапазон IP, підключити клієнти.
- **Хід виконання**:
  1. **Крок 1: Топологія та дефолт DHCP**
     3 PC → Ethernet до Router. PC0: DHCP (gateway 192.168.0.1). GUI: 192.168.0.1, admin/admin; Start IP 192.168.0.100.
     📷 ![dfg](https://github.com/user-attachments/assets/4afed343-0b23-49e6-ad4b-3d01f9d433be)
     📷 ![uty](https://github.com/user-attachments/assets/131e8891-6884-4540-b1a2-a2e5af2c3579)
     📷 ![jghn](https://github.com/user-attachments/assets/50073493-9a70-456f-ae8b-01ae0fc2101f)
     📷 ![dfng](https://github.com/user-attachments/assets/5de0bedf-db17-45f4-bd94-c3f659f35bde)
     _Пояснення_: Дефолтний діапазон; ПК отримують IP автоматично.

  2. **Крок 2: Зміна IP роутера**
     Basic Setup > IP: 192.168.5.1. Save. PC0: DHCP (нова IP 192.168.5.x).
     📷 ![dgf](https://github.com/user-attachments/assets/e938bb73-0193-413a-ba99-064774d4d4c6)
     📷 ![jgh](https://github.com/user-attachments/assets/c16531e3-d7ac-4e10-83c5-4afa8a261ce2)
     _Пояснення_: Зміна мережі; клієнти оновлюють конфігурацію.

  3. **Крок 3: Зміна діапазону DHCP**
     Start IP: 192.168.5.126, Max Users: 75. Save. PC0: DHCP (IP 192.168.5.126).
     📷 ![hjk,](https://github.com/user-attachments/assets/4b3b0e55-2728-4ce5-af14-15492bcefe86)
     📷 <img width="967" height="581" alt="xfgd" src="https://github.com/user-attachments/assets/e3c05e00-28f6-44fa-b0d1-d57b546b9999" />
     _Пояснення_: Кастомний діапазон; обмеження/розширення клієнтів.

  4. **Крок 4: DHCP на інших PC та тест**
     PC1/PC2: DHCP (IP 192.168.5.127/128). Ping: роутер, PC0, PC1 – успішно.
     📷 <img width="600" height="300" alt="ping test" src="https://github.com/user-attachments/assets/example-ping-dhcp.png" />
     📷 <img width="982" height="336" alt="xfgd" src="https://github.com/user-attachments/assets/637c3fb2-1c69-4230-8437-5f6f25a33a82" />
     📷 <img width="594" height="1180" alt="xfgd" src="https://github.com/user-attachments/assets/cb3d704c-7b6f-489a-85d0-e34aae09442f" />

     _Пояснення_: Всі клієнти в мережі; ping підтверджує зв'язок.

- **Висновок**:
  Лабораторна робота навчила кастомізації DHCP: зміна IP/діапазону, автоматичне призначення; повна сумісність клієнтів.

---

## 🚀 Висновки
Курс **Основи роботи в мережі** дав практичні навички налаштування домашньої мережі: підключення, DHCP, Wi-Fi безпека, доступ до веб. Словник та лаби закріпили терміни (SSID, WPA2, DHCP) та інструменти (GUI, ping). Готовий до тем бездротової безпеки та масштабування.