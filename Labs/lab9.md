# 📋 ЛАБОРАТОРНА РОБОТА №9

## 📌 Дисципліна: "Хмарні технології та сервіси"

## 🏷 Тема:
> Створення віртуальних машин у середовищі Google Cloud Platform

## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б

---

## 🎯 Мета роботи
1. Ознайомитися з сервісом Google Compute Engine (GCE) у складі Google Cloud Platform (GCP).
2. Навчитися створювати та налаштовувати віртуальні машини (VM) на Linux та Windows.
3. Освоїти підключення до VM через SSH (Linux) та RDP (Windows).
4. Виконати практичні завдання з налаштування вебсервера Nginx та управління VM.

## 🛠 Матеріальне забезпечення
- 💻 Браузер з доступом до мережі Інтернет.
- 🌐 Сайт Google Cloud Platform: [console.cloud.google.com](https://console.cloud.google.com).
- Google Cloud SDK (CLI) для виконання команд.
- SSH-клієнт (для Linux VM).
- Remote Desktop Connection (для Windows VM).

---

## 📚 Попередня підготовка: Відповіді на питання
### 2.1. Для чого призначений сервіс Google Compute Engine (GCE) у складі Google Cloud Platform?
**Google Compute Engine (GCE)** – сервіс для створення, налаштування та запуску віртуальних машин у хмарі GCP. Використовується для:
- Розгортання серверів для веб-додатків, баз даних, аналітики.
- Гнучкого масштабування обчислень.
- Тестування та розробки програмного забезпечення.
- Запуску контейнерів або високопродуктивних обчислень (HPC).

### 2.2. Що таке Machine Images у GCP? Чим відрізняються стандартні образи, надані Google, від користувацьких (Custom Images)?
**Machine Images** – це шаблони операційних систем або попередньо налаштованих середовищ для швидкого розгортання VM.
- **Стандартні образи**: Надаються Google через Cloud Marketplace (наприклад, Ubuntu, Windows Server). Регулярно оновлюються, підходять для типових задач.
- **Користувацькі образи (Custom Images)**: Створюються користувачем на основі існуючої VM. Містять специфічні налаштування, встановлене ПЗ чи конфігурації. Використовуються для повторного розгортання однакових VM.

### 2.3. Для чого використовуються Persistent Disks у GCP? Які існують типи дисків та у чому їхні відмінності (Standard, Balanced, SSD)?
**Persistent Disks** – керовані блокові сховища для VM, що забезпечують надійне зберігання даних.
- **Типи дисків**:
  - **Standard (HDD)**: Найдешевший, для некритичних задач (бекапи, архіви).
  - **Balanced (SSD)**: Баланс між вартістю та продуктивністю, для стандартних застосунків (вебсервери).
  - **SSD (Performance)**: Висока швидкість для критичних задач (бази даних, аналітика).
- **Відмінності**: Standard – низька швидкість, низька ціна; Balanced – середня продуктивність; SSD – висока швидкість, вища ціна.

### 2.4. Що таке Snapshots у Google Cloud? У яких випадках їх доцільно створювати та використовувати?
**Snapshots** – знімки дисків VM для створення резервних копій у певний момент часу. Використовуються для:
- Резервного копіювання перед оновленнями чи змінами.
- Відновлення VM після збоїв.
- Створення нових VM із попередніми налаштуваннями.
- Міграції даних між регіонами.

### 2.5. Перелічіть основні типи віртуальних машин (Machine Types) у GCP. Коли доцільно використовувати кожен тип (e2, n2, n2-highmem, n2-highcpu тощо)?
- **e2**: Загального призначення, економічні. Для студентських проєктів, невеликих вебсерверів.
- **n2**: Універсальні, баланс CPU та пам’яті. Для бізнес-додатків, баз даних.
- **n2-highmem**: Пам’яттєво оптимізовані. Для великих баз даних, кешування.
- **n2-highcpu**: Обчислювально оптимізовані. Для аналітики, машинного навчання.
- **c2, g2**: Для високопродуктивних обчислень (HPC, рендеринг).

### 2.6. Які дистрибутиви операційних систем доступні у шаблонах Google Cloud Free Tier? Наведіть приклади для сімейств Windows і Linux.
- **Linux**: Ubuntu 22.04 LTS, Debian 11, CentOS 9 (доступні в Free Tier, наприклад, e2-micro).
- **Windows**: Windows Server 2019 Datacenter, Windows Server 2022 (обмежено Free Tier через вищі вимоги до ресурсів).
- **Примітка**: Free Tier дозволяє використовувати e2-micro з 30 ГБ Standard Disk для Linux, але Windows може вимагати платних ресурсів.

### 2.7. Яке призначення мають Firewall rules у GCP і як вони впливають на доступ до віртуальної машини?
**Firewall Rules** визначають, які вхідні та вихідні з’єднання дозволені для VM:
- Дозволяють/блокують трафік за протоколами (TCP, UDP), портами (80, 443, 3389) чи IP-адресами.
- Впливають на доступ: наприклад, дозвіл HTTP (порт 80) відкриває веб-доступ, а RDP (3389) – віддалений доступ до Windows.

### 2.8. У чому різниця між підключенням до віртуальної машини через SSH та через RDP? У яких випадках використовується кожен спосіб?
- **SSH**: Безпечний протокол для Linux VM. Використовується для командного рядка, конфігурації серверів чи виконання скриптів. Потребує SSH-ключів або пароля.
- **RDP**: Протокол для Windows VM. Надає графічний інтерфейс для віддаленого керування. Використовується для адміністрування Windows-додатків чи GUI.

---

## 📋 Хід роботи
### 1. Авторизація в Google Cloud Console
- Увійшов до Google Cloud Console ([console.cloud.google.com](https://console.cloud.google.com)) за допомогою Google Account.
- Активував Free Trial (отримав $300 кредитів на 90 днів).

<img width="2560" height="1248" alt="dsf" src="https://github.com/user-attachments/assets/1fcd269d-364e-49e5-a954-61f7f27927e9" />
<img width="1284" height="856" alt="dsf" src="https://github.com/user-attachments/assets/3b91f8b6-8f2a-4497-8acd-ea9d65e42cd2" />
<img width="1273" height="1166" alt="dsf" src="https://github.com/user-attachments/assets/34c699da-0b1e-4c8b-b861-c969962cc61f" />

### Практичне завдання №1. Віртуальна машина Linux
#### 2. Створення віртуальної машини Linux
- Перейшов до **Compute Engine** → **VM instances** → **Create Instance**.
- Налаштування:
  - **Назва VM**: Linux_Nagornyi_IM_RPZ24B
  - **Region**: europe-west1
  - **Zone**: europe-west1-b
  - **Machine type**: e2-micro (Free Tier)
  - **Boot disk**: Ubuntu 22.04 LTS
  - **Firewall**: Allow HTTP traffic, Allow HTTPS traffic

<img width="956" height="534" alt="изображение" src="https://github.com/user-attachments/assets/84799925-dc0c-4a27-ae51-7687dec06a50" />
<img width="480" height="261" alt="изображение" src="https://github.com/user-attachments/assets/31966ce9-a403-4371-b468-442c6dac574f" />
<img width="402" height="506" alt="изображение" src="https://github.com/user-attachments/assets/5089df35-d14d-4479-a06e-473d7729c5a6" />
<img width="1077" height="771" alt="изображение" src="https://github.com/user-attachments/assets/1c1b2f83-6207-4532-8adb-73d0996f02a7" />
<img width="885" height="84" alt="изображение" src="https://github.com/user-attachments/assets/2b96861b-8231-4efb-b819-605227a5be60" />


#### 3. Налаштування Startup Script
- У розділі **Management** → **Automation** → **Startup script** вставив:
```bash
#!/bin/bash
apt-get update -y
apt-get install -y nginx
systemctl enable nginx
systemctl start nginx
```

<img width="893" height="604" alt="firefox_tOT27HdXhX" src="https://github.com/user-attachments/assets/d90be2b1-f5b4-4e00-b2ce-369969fcf585" />


#### 4. Створення та перевірка VM
- Натиснув **Create** і дочекався розгортання VM.
- Знайшов External IP у властивостях VM.
- Відкрив IP у браузері – побачив стартову сторінку Nginx.

<img width="1588" height="466" alt="изображение" src="https://github.com/user-attachments/assets/8c4b0d46-077d-4210-b76b-c0bd15a27785" />


#### 5. Перевірка через Cloud Shell
- Відкрив Cloud Shell і виконав:
```bash
gcloud compute instances list
```
- Підключився до VM через SSH:
```bash
gcloud compute ssh Linux_Nagornyi_IM_RPZ24B --zone=europe-west1-b
```

<img width="1295" height="436" alt="изображение" src="https://github.com/user-attachments/assets/d0ee69b0-f57f-4a2a-95c1-40b714be4d71" />
<img width="1365" height="328" alt="изображение" src="https://github.com/user-attachments/assets/32a0b7a5-c037-42b6-b430-cd353b1a9090" />


#### 6. Налаштування Nginx
- Через SSH підключився до VM:
```bash
gcloud compute ssh Linux_Nagornyi_IM_RPZ24B --zone=europe-west1-b
```
- Відредагував конфігураційний файл Nginx (`/etc/nginx/sites-available/default`):
```bash
sudo nano /etc/nginx/sites-available/default
```
- Створив HTML-сторінку `/var/www/html/index.html`:
```html
<!DOCTYPE html>
<html lang="uk">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Welcome to RPZ-24!</title>
  <style>
    body {
      background-color: #111;
      color: #ddd;
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 10%;
    }
    h1 {
      color: #fff;
      font-size: 2.5em;
    }
    a {
      color: #4ea3ff;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
    .info {
      margin-top: 40px;
      color: #ff5555;
      font-size: 1.2em;
    }
  </style>
</head>
<body>
  <h1>Welcome to RPZ-24!</h1>
  <p>If you see this page, the Nginx web server is successfully installed and working.</p>
  <p>For online documentation, refer to <a href="https://nginx.org">nginx.org</a>.</p>
  <div class="info">Team Info: РПЗ-24 — Нагорний Ілля</div>
</body>
</html>
```
- Перезапустив Nginx:
```bash
sudo systemctl restart nginx
```
- Перевірив сторінку у браузері.
<img width="1059" height="434" alt="499035481-6a017588-14d8-41b6-b339-74c3e11ef990" src="https://github.com/user-attachments/assets/f77f5bcd-d273-4d1c-a0fc-af91dc9e03df" />


#### 7. Зупинка та видалення VM
- Через Google Cloud Console:
  - Зупинив: **Compute Engine** → **VM instances** → **Linux_Nagornyi_IM_RPZ24B** → **Stop**.
  - Видалив: **Delete**.
- Через Cloud Shell:
```bash
gcloud compute instances stop Linux_Nagornyi_IM_RPZ24B --zone=europe-west1-b
gcloud compute instances delete Linux_Nagornyi_IM_RPZ24B --zone=europe-west1-b --quiet
```
- **Відмінності**:
  - **Stop**: Зупиняє VM, звільняє CPU/RAM, але зберігає диски та IP. Плата за обчислення припиняється.
  - **Delete**: Видаляє VM і всі пов’язані ресурси (диски, IP).

<img width="1515" height="206" alt="изображение" src="https://github.com/user-attachments/assets/e920fc5f-27af-4b2e-b3ae-16e2deed3122" />

### Практичне завдання №2. Віртуальна машина Windows Server
#### 8. Створення віртуальної машини Windows
- Перейшов до **Compute Engine** → **VM instances** → **Create Instance**.
- Налаштування:
  - **Назва VM**: Windows_Nagornyi_IM_RPZ24B
  - **Region**: europe-west1
  - **Zone**: europe-west1-b
  - **Machine type**: e2-micro (Free Tier)
  - **Boot disk**: Windows Server 2019 Datacenter
  - **Firewall**: Allow RDP (3389)

<img width="1077" height="771" alt="изображение" src="https://github.com/user-attachments/assets/1c1b2f83-6207-4532-8adb-73d0996f02a7" />

#### 9. Підключення через RDP
- У властивостях VM натиснув **Set Windows password**, отримав логін і пароль.
- Відкрив Remote Desktop Connection, ввів External IP, логін і пароль.
- Успішно підключився.

<img width="1472" height="1034" alt="j" src="https://github.com/user-attachments/assets/4707cf7a-16d1-4aff-80f6-c6fc9a2c54f6" />
<img width="635" height="415" alt="ckdzrvbqw-k2scjehrdvn3jsins" src="https://github.com/user-attachments/assets/e4aab307-dfb2-4d37-8a54-d97dba0eae67" />

#### 10. Зміна імені сервера
- Увійшов до VM, відкрив **This PC** → **Properties**.
- Змінив ім’я сервера: **Settings** → **System** → **About** → **Rename this PC** → WSERVER_RPZ24B.
- Перезавантажив VM.
- Повторно підключився через RDP, перевірив зміну імені.

<img width="830" height="301" alt="image" src="https://github.com/user-attachments/assets/76d6917c-6f59-440d-8dbe-303effa38b45" />

#### 11. Зупинка та видалення Windows VM
- Через Google Cloud Console:
  - Зупинив: **Stop Instance**.
  - Видалив: **Delete Instance**.
- Через Cloud Shell:
```bash
gcloud compute instances stop Windows_Nagornyi_IM_RPZ24B --zone=europe-west1-b
gcloud compute instances delete Windows_Nagornyi_IM_RPZ24B --zone=europe-west1-b --quiet
```

<img width="1515" height="206" alt="изображение" src="https://github.com/user-attachments/assets/e920fc5f-27af-4b2e-b3ae-16e2deed3122" />

---

## ❓ Контрольні питання
1. **Яку роль відіграють SSH-ключі та паролі при підключенні до віртуальних машин у GCP?**
   SSH-ключі (для Linux) забезпечують безпечний доступ через пару ключів (публічний/приватний). Паролі (для Windows/Linux) – простіший, але менш безпечний метод автентифікації.

2. **Яка команда використовується для підключення до Linux-віртуальної машини через gcloud CLI?**
```bash
gcloud compute ssh <vm-name> --zone=<zone-name>
```
Наприклад: `gcloud compute ssh Linux_Nagornyi_IM_RPZ24B --zone=europe-west1-b`.

3. **Які способи підключення доступні для Linux-VM у GCP?**
   - Через SSH у Cloud Shell або терміналі (`gcloud compute ssh`).
   - Через браузер (кнопка SSH у Google Cloud Console).
   - Через SSH-клієнт (наприклад, PuTTY) із використанням External IP.

4. **Як можна підключитися до Windows-віртуальної машини у GCP?**
   Через Remote Desktop Protocol (RDP) за допомогою Remote Desktop Connection, ввівши External IP, логін і пароль. Альтернатива – через браузер із GCP Console (RDP-клієнт).

5. **У чому полягає різниця між станами Stop і Delete для віртуальної машини?**
   - **Stop**: Зупиняє VM, звільняє обчислювальні ресурси, але зберігає диски та IP. Плата стягується лише за сховище.
   - **Delete**: Повністю видаляє VM і пов’язані ресурси, припиняючи всі нарахування.

6. **Для чого використовується Startup script під час створення VM?**
   **Startup script** виконує команди під час запуску VM для автоматизації налаштувань (наприклад, встановлення ПЗ, оновлення системи, конфігурація сервісів).

7. **Як у GCP можна дозволити або заборонити вхідний трафік до віртуальної машини?**
   Через **Firewall Rules** у розділі **VPC network** → **Firewall**. Створюються правила, що дозволяють/блокують трафік за портами, протоколами чи IP-адресами.

---

## 📝 Висновки
Лабораторна робота №9 дозволила ознайомитися з процесом створення та управління віртуальними машинами в Google Compute Engine. Виконано налаштування Linux VM (Ubuntu) із встановленням Nginx та кастомізацією веб-сторінки, а також Windows Server VM зі зміною імені сервера. Освоєно підключення через SSH і RDP, керування через Google Cloud Console та gcloud CLI. Робота поглибила розуміння хмарних технологій, зокрема GCE, Firewall Rules, Persistent Disks та Snapshots.

---

## 🔗 Корисні посилання
- [Google Cloud Console](https://console.cloud.google.com)
- [Google Cloud SDK Documentation](https://cloud.google.com/sdk/docs)
- [How to Create a Linux VM Instance on Google Cloud Platform](https://youtu.be/example)
- [How to Create a Windows VM in Google Cloud Platform & Connect via RDP](https://youtu.be/example)
- [Google Cloud Skills Boost](https://www.cloudskillsboost.google)

## 🎯 Система оцінювання
- 📚 Питання попередньої підготовки: 5 балів
- 📋 Практичне завдання №1 (Linux VM): 5 балів
- 📋 Практичне завдання №2 (Windows VM): 5 балів
- ❓ Контрольні питання та висновки: 5 балів
- 🌐 Використання англійської мови (фрагментарно): +5 балів