# 📌 Комп'ютерні мережі

## 🏷 Курс: «Мережеві пристрої та початкова конфігурація» (Комп'ютерні мережі)

## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б

---

## 🎯 Мета роботи
1. Зареєструватися на курс netacad.com, пройти модулі та отримати сертифікат.
2. Додати матеріали курсу до Git-репозиторію або Google-сайту «Комп'ютерні мережі».
3. Виділити 10 нових термінів у таблиці: англ. / укр. / пояснення.
4. Підготувати звіти з 3 лабораторних робіт (7.1.9, 10.3.3, 11.4.5) зі скріншотами ключових кроків та поясненнями.

## 🛠 Матеріальне забезпечення
- 💻 Комп’ютер з Cisco Packet Tracer (остання версія).
- 🌐 Доступ до Cisco Networking Academy (netacad.com).
- 📚 Матеріали курсу «Мережеві пристрої та початкова конфігурація».

---

## 📚 Короткі теоретичні відомості
Курс знайомить з основами мережевих пристроїв Cisco: комутаторами, маршрутизаторами, початковою конфігурацією IOS. Вивчаються протоколи ARP, DNS, команди show, усунення типових проблем (шлюз за замовчуванням). Практика в Packet Tracer дозволяє симулювати реальні топології, аналізувати трафік, конфігурувати інтерфейси та перевіряти зв’язок без фізичного обладнання.

---

## 📋 Зміст роботи

### 1. Сертифікат курсу

[]()

### 2. Словник термінів
Нижче наведено таблицю з 10 новими термінами, вивченими в курсі.
| Термін (англ.) | Термін (укр.) | Визначення (пояснення) |
|---------------------------|---------------------------|---------------------------------------------------------------------------------------|
| ARP (Address Resolution Protocol) | ARP (Протокол розв’язання адрес) | Протокол для зіставлення IP-адреси з MAC-адресою в локальній мережі (7.1.9). |
| ARP Table | Таблиця ARP | Таблиця на пристрої, що зберігає пари IP–MAC для швидкого доступу без широкомовних запитів. |
| MAC Address Table | Таблиця MAC-адрес | Таблиця на комутаторі, що зіставляє MAC-адреси з портами для ефективної пересилки кадрів. |
| Default Gateway | Шлюз за замовчуванням | IP-адреса маршрутизатора, до якого надсилаються пакети для віддалених мереж. |
| Cisco IOS | Cisco IOS | Операційна система Cisco для конфігурації та керування мережевими пристроями. |
| show commands | Команди show | Набір команд IOS для відображення стану інтерфейсів, маршрутів, ARP тощо (10.3.3). |
| PDU (Protocol Data Unit) | Одиниця даних протоколу | Пакет даних на певному рівні моделі OSI, що аналізується в симуляції Packet Tracer. |
| Simulation Mode | Режим симуляції | Режим Packet Tracer для покрокового аналізу трафіку та PDU. |
| VLAN Interface | Інтерфейс VLAN | Віртуальний інтерфейс на комутаторі для керування (наприклад, VLAN 1 з IP). |
| Troubleshooting | Усунення неполадок | Методичний процес пошуку та виправлення проблем у мережі (11.4.5). |

### 3. Звіти лабораторних робіт
Нижче наведено звіти з виконаних лабораторних робіт. Для кожної наведено скріншоти ключових кроків (у репозиторії – як зображення) та короткі пояснення.

#### Лабораторна робота 7.1.9: Packet Tracer – Дослідження ARP-таблиці
- **Мета**:
  Дослідити ARP-запити, таблицю ARP на хостах та маршрутизаторі, таблицю MAC-адрес на комутаторах, а також ARP-процес для віддаленого зв’язку.
- **Хід виконання**:

  ![](https://github.com/user-attachments/assets/b480ed09-839d-425a-82ab-e35511070cb8)

| Device        | Interface | MAC Address       | Switch Interface |
|---------------|-----------|-------------------|------------------|
| Router0       | Gg0/0     | 0001.6458.2501    | G0/1             |
|               | S0/0/0    | N/A               | N/A              |
| Router1       | G0/0      | 00E0.F7B1.8901    | G0/1             |
|               | S0/0/0    | N/A               | N/A              |
| 10.10.10.2    | Wireless  | 0060.2F84.4AB6    | F0/2             |
| 10.10.10.3    | Wireless  | 0060.4706.572B    | F0/2             |
| 172.16.31.2   | F0        | 000C.85CC.1DA7    | F0/1             |
| 172.16.31.3   | F0        | 0060.7036.2849    | F0/2             |
| 172.16.31.4   | G0        | 0002.1640.8D75    | F0/3             |

  1. **Крок 1: Генерація ARP-запитів пінгом 172.16.31.3 з 172.16.31.2**
     -. На 172.16.31.2: Command Prompt → `arp -d` (очистити таблицю).  
     -. У Simulation mode: `ping 172.16.31.3`. З’являються 2 PDU (ICMP чекає ARP).  
     -. Capture/Forward: ARP broadcast рухається до Switch1, ICMP зникає.  
     <img width="319" height="115" alt="d" src="https://github.com/user-attachments/assets/4f0c7e9d-f45e-4966-8f86-3f0d5c501436" />
     
     _Пояснення_: Пінг не може завершитися без MAC одержувача, тому надсилається ARP broadcast.

  2. **Крок 2: Аналіз PDU та копій**
     -. Destination MAC у PDU: не вказано в таблиці (broadcast).  
     -. Switch1 робить 3 копії PDU.  
     -. Приймає 172.16.31.3. У відповіді: source → destination, broadcast → MAC 172.16.31.3.  
     -. Switch1 робить 1 копію під час відповіді.
     <img width="207" height="462" alt="d" src="https://github.com/user-attachments/assets/ace945b6-3f67-4975-a466-6ce25a5ed8d8" />
     <img width="551" height="422" alt="d" src="https://github.com/user-attachments/assets/1edf594a-0658-4867-a806-475aad9e8d86" />
     <img width="393" height="190" alt="d" src="https://github.com/user-attachments/assets/226ef5c6-ba98-46af-a309-e1f60b974974" />

     _Пояснення_: Комутатор розмножує broadcast на всі порти (окрім вхідного).
     
  4. **Крок 3: Перевірка таблиці ARP**
     -. ICMP PDU повертається, MAC узгоджені з IP.  
     -. Realtime: пінг завершується. `arp -a` → MAC відповідає 172.16.31.3.
     <img width="409" height="54" alt="d" src="https://github.com/user-attachments/assets/e1e01355-9dbc-4af0-8413-4475e451ee70" />
     
     _Пояснення_: ARP-запит видається, коли MAC невідомий.
     
  6. **Крок 4: Заповнення MAC-таблиці комутатора**
     -. Пінг 172.16.31.4 з 172.16.31.2 та 10.10.10.3 з 10.10.10.2 (4 успішні відповіді).  
     <img width="413" height="184" alt="d" src="https://github.com/user-attachments/assets/89975e5d-de12-42cf-8bbf-02df0512f85d" />
     <img width="405" height="240" alt="d" src="https://github.com/user-attachments/assets/6d13f244-119f-4e82-84a5-890448300ebf" />

     _Пояснення_: Додатковий трафік заповнює таблицю.
     
  7. **Крок 5: Перегляд MAC-таблиці**
     -. На Switch1/Switch0: `show mac-address-table` → записи відповідають топології. Два MAC на одному порту – через Access Point.  
     <img width="351" height="171" alt="d" src="https://github.com/user-attachments/assets/6cf3888e-56f9-4380-9657-5cbf145b23f7" />

     _Пояснення_: Комутатор вчиться, звідки приходять кадри.
     
  8. **Крок 6: ARP для віддаленого зв’язку**
     -. Пінг 10.10.10.1 з 172.16.31.2 → нова запись ARP: 172.16.31.1 (шлюз).  
     -. В Simulation: ARP до шлюзу (172.16.31.1), а не до 10.10.10.1.  
     <img width="429" height="445" alt="d" src="https://github.com/user-attachments/assets/2dc2b331-78f7-42c8-bcda-203824001f3f" />

     _Пояснення_: Хост використовує ARP до шлюзу для віддалених мереж.
     
  9. **Крок 7: ARP на маршрутизаторі**
     -. На Router1: `show mac-address-table` → 0 (команда для комутатора). `show arp` → запис для 172.16.31.2. Перший пінг таймаутить.  
     <img width="583" height="167" alt="d" src="https://github.com/user-attachments/assets/f4a2b083-773f-4b6c-a884-8121ca6a34f8" />

     _Пояснення_: Маршрутизатор відповідає на ARP, але перший пакет втрачається.
     
- **Висновок**:
  Робота показала механізм ARP: broadcast-запити, заповнення таблиць, відмінності локального/віддаленого зв’язку. Це основа для розуміння L2/L3 взаємодії.

#### Лабораторна робота 10.3.3: Packet Tracer – Використання команд show Cisco IOS
- **Мета**:
  Підключитися до маршрутизатора ISP та дослідити команди show в User EXEC та Privileged EXEC режимах.
- **Хід виконання**:

  ![](https://github.com/user-attachments/assets/abba719d-31c5-4a27-8b48-7ab372b47e10)

  1. **Крок 1: Підключення до ISPRouter**
     а. ISP PC → Desktop → Terminal (налаштування за замовчуванням) → OK.  
     б. Промпт `ISPRouter>`.  
     ![](https://github.com/user-attachments/assets/aac4ff82-9e9d-4c76-b23a-8d435b67dd7e)
     ![](https://github.com/user-attachments/assets/3a29d222-1c36-472c-b5f7-78e60acbbf91)

     _Пояснення_: Термінал емулює консольне з’єднання.
     
  2. **Крок 2: Команди show в User EXEC**
     -. `show ?` → приклади: cdp, class-map, clock.  
     -. `show arp` → MAC/IP: 0001.96CD.2501 – 209.165.201.1 тощо.
     <img width="1589" height="149" alt="d" src="https://github.com/user-attachments/assets/8fa16eb5-94fe-4be4-a84a-1130fcc2bcef" />

     -. `show flash` → IOS: isr4300-universalk9.03.16.05.S.155-3.S5-ext.SPA.bin.
     <img width="1200" height="377" alt="d" src="https://github.com/user-attachments/assets/6a3b3c65-4236-4944-a2ae-e46a6c073793" />

     -. `show ip route` → 2 маршрути.
     <img width="1635" height="685" alt="d" src="https://github.com/user-attachments/assets/59de6566-cbd6-4862-a8d2-50a465115af8" />

     -. `show interfaces` → GigabitEthernet0/0/0 Up/Up.
     <img width="1726" height="934" alt="d" src="https://github.com/user-attachments/assets/3e9b1e65-ff05-4350-89ba-e168e1980cd9" />

     -. `show ip interface` → підключений GigabitEthernet0/0/0.
     <img width="1554" height="308" alt="d" src="https://github.com/user-attachments/assets/fa0843b8-5b6e-4bc2-b721-d6fc67f6d09f" />

     -. `show version` → пакети ipbasek9, securityk9.
     <img width="1720" height="973" alt="d" src="https://github.com/user-attachments/assets/4d60cd17-2ef2-4540-b9b8-6ad9ce172420" />
 
     -. `show protocols` → IP routing увімкнено на G0/0/0.
     <img width="924" height="227" alt="d" src="https://github.com/user-attachments/assets/bf207a76-b1e7-45bf-aaa9-013664f741de" />

     -. `show running-config` → помилка (потрібен Privileged).  
     _Пояснення_: User EXEC – лише перегляд базової інформації.
     
  4. **Крок 3: Перехід до Privileged EXEC**
     -. `enable` → `ISPRouter#`. `show ?` → додаткові: aaa, access-list, file.  
     -. `show running-config` → повна конфігурація.  
     _Пояснення_: Privileged дозволяє переглядати/змінювати конфіг.
     
- **Висновок**:
  Команди show – ключовий інструмент діагностики: від ARP до повної конфігурації. Різні режими обмежують доступ для безпеки.

#### Лабораторна робота 11.4.5: Packet Tracer – Усунення неполадок шлюзу за замовчуванням
- **Мета**:
  Завершити документацію мережі, ізолювати проблеми зв’язку, запропонувати/реалізувати рішення, перевірити та задокументувати.
- **Хід виконання**:

  ![10 3 5-Packet-Tracer-Troubleshoot-Default-Gateway-Issues-ILM](https://github.com/user-attachments/assets/add435df-826a-4f17-8249-8d444a1b9f70)

| Device | Interface | IP Address     | Subnet Mask       | Default Gateway |
|--------|-----------|----------------|-------------------|-----------------|
| R1     | G0/0      | 192.168.10.1   | 255.255.255.0     | N/A             |
|        | G0/1      | 192.168.11.1   | 255.255.255.0     | N/A             |
| S1     | VLAN 1    | 192.168.10.2   | 255.255.255.0     | 192.168.10.1    |
| S2     | VLAN 1    | 192.168.11.2   | 255.255.255.0     | 192.168.11.1    |
| PC1    | NIC       | 192.168.10.10  | 255.255.255.0     | 192.168.10.1    |
| PC2    | NIC       | 192.168.10.11  | 255.255.255.0     | 192.168.10.1    |
| PC3    | NIC       | 192.168.11.10  | 255.255.255.0     | 192.168.11.1    |
| PC4    | NIC       | 192.168.11.11  | 255.255.255.0     | 192.168.11.1    |

  1. **Крок 1: Доповнення документації**
     -. Заповнити Default Gateway: S1/S2, PC – з таблиці.  
     <img width="213" height="65" alt="d" src="https://github.com/user-attachments/assets/fe118f3d-8a5f-42d4-90ea-35d3c1ecdb3d" />
     <img width="691" height="732" alt="d" src="https://github.com/user-attachments/assets/7ef2ce24-9b0b-4649-9ead-cfb3fbfcce8c" />

     _Пояснення_: Точна документація – основа troubleshooting.
     
  2. **Крок 2: Локальні тести**
     -. PC1–PC2: ні (IP PC1 неправильна).  
     -. PC1–S1, PC1–R1: документувати.  
     []()  
     _Пояснення_: Спочатку локальний доступ.
     
  3. **Крок 3: Віддалені тести**
     -. PC1–PC4: після локальних виправлень.  
     _Пояснення_: End-to-end після локального.
     
  4. **Крок 4: Виявлені проблеми та рішення**
     -. PC1: неправильна IP → змінити на 192.168.10.10.  
     -. S2: відсутня IP → 192.168.11.2/24, DG 192.168.11.1.  
     -. PC4: неправильний DG → 192.168.11.1.  
     -. S1: відсутній DG → 192.168.10.1.  
     <img width="899" height="655" alt="d" src="https://github.com/user-attachments/assets/b47150b2-0ac7-43cc-9a2d-49631e6e5db3" />
  
     _Пояснення_: Перевірка ipconfig / show ip interface brief.
     
  5. **Крок 5: Реалізація**
     -. Змінити IP/DG на PC1, PC4, S1, S2 через Desktop → IP Configuration або CLI.  
     <img width="827" height="634" alt="d" src="https://github.com/user-attachments/assets/c5edf316-63bf-4417-95c7-eab0178b6526" />
     <img width="765" height="618" alt="d" src="https://github.com/user-attachments/assets/0623124a-379f-45d8-927b-38f17b027a81" />

     _Пояснення_: Одна зміна за раз.
     
  6. **Крок 6: Перевірка**
     -. Пінг PC1–PC2, PC1–PC4, S1–будь-який: успішно.  
     <img width="942" height="679" alt="d" src="https://github.com/user-attachments/assets/5ea32ea9-c9aa-49c9-b120-759b76c977b4" />
     <img width="1040" height="724" alt="d" src="https://github.com/user-attachments/assets/548737e3-e9d8-46a3-91ae-0a57f4c849a0" />

     _Пояснення_: Повтор тестів підтверджує.
     
- **Висновок**:
  Методичний підхід (документація → ізоляція → рішення → перевірка) ефективно вирішує проблеми шлюзу. Ключ – точна адресація та DG.

---

## 🚀 Висновки
Курс дав практичні навички роботи з Cisco IOS: ARP-механіка, діагностика show-командами, усунення типових помилок конфігурації. Packet Tracer – потужний інструмент для симуляції та відпрацювання реальних сценаріїв без обладнання.