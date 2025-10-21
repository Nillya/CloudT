# 📋 ЛАБОРАТОРНА РОБОТА №7

## 📌 Дисципліна: "Хмарні технології та сервіси"

## 🏷 Тема:
> Створення віртуальних машин у середовищі Azure

## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б

---

## 🎯 Мета роботи
1. Ознайомитися з хмарним провайдером Azure, зокрема з сервісом Azure Virtual Machines.
2. Навчитися створювати та налаштовувати віртуальні машини (VM) у Azure.
3. Освоїти підключення до VM через SSH (Linux) та RDP (Windows).
4. Виконати практичні завдання з налаштування VM та управління ресурсами.

## 🛠 Матеріальне забезпечення
- 💻 Браузер з доступом до мережі Інтернет.
- 🌐 Сайт Azure: [portal.azure.com](https://portal.azure.com).
- Azure CLI (встановлено на ПК).
- SSH-клієнт (для Linux VM).
- Remote Desktop Connection (для Windows VM).

---

## 📚 Попередня підготовка: Відповіді на питання

### 2.1. Для чого потрібні Azure Marketplace Images? Чим відрізняються готові публічні образи від приватних образів, створених користувачем (Custom Images)?
**Azure Marketplace Images** – це попередньо налаштовані шаблони операційних систем та програмного забезпечення, доступні для швидкого розгортання віртуальних машин. Вони включають популярні ОС (Windows, Ubuntu, CentOS) та додатки (вебсервери, бази даних).  
**Відмінності**:
- **Публічні образи**: Створюються Microsoft або партнерами, регулярно оновлюються, підходять для стандартних сценаріїв. Наприклад, Ubuntu Server 22.04 LTS із базовим набором ПЗ.
- **Приватні образи (Custom Images)**: Створюються користувачем на основі існуючої VM, містять специфічні налаштування, встановлене ПЗ чи конфігурації. Використовуються для повторного розгортання ідентичних VM у проєктах.

### 2.2. Для чого потрібні Azure Managed Disks? Які типи дисків підтримуються в Azure?
**Azure Managed Disks** – це керовані диски, що використовуються для зберігання даних віртуальних машин. Вони спрощують управління, забезпечують автоматичне масштабування та шифрування.  
**Типи дисків**:
- **Ultra Disk**: Найвища продуктивність для інтенсивних робочих навантажень (бази даних, аналітика).
- **Premium SSD**: Висока швидкість для продуктивних застосунків (вебсервери, ERP).
- **Standard SSD**: Баланс між вартістю та продуктивністю для стандартних задач.
- **Standard HDD**: Найдешевший варіант для некритичних даних (архіви, резервні копії).

### 2.3. Для чого використовуються Snapshots в Azure? У яких випадках їх доцільно використовувати?
**Snapshots** – це знімки дисків VM для створення резервних копій у певний момент часу. Вони дозволяють відновлювати дані або створювати нові VM на основі знімка.  
**Випадки використання**:
- Резервне копіювання перед оновленням системи чи ПЗ.
- Тестування конфігурацій із можливістю швидкого повернення до попереднього стану.
- Міграція даних між регіонами чи створення клонів VM.

### 2.4. Перерахуйте основні типи віртуальних машин (VM sizes) у Azure. Коли доцільно використовувати кожен з них?
**Типи VM sizes**:
- **Загального призначення (B, D)**: Баланс CPU та пам’яті. Для вебсерверів, невеликих баз даних, тестування. Наприклад, B1s – для Free Tier.
- **Обчислювально оптимізовані (F)**: Висока продуктивність CPU. Для обробки великих обсягів даних, аналітики.
- **Пам’яттєво оптимізовані (E, M)**: Великий обсяг RAM. Для баз даних, кешування.
- **GPU-оптимізовані (NV, NC)**: Для машинного навчання, рендерингу, обробки графіки.
- **Високопродуктивні (H)**: Для HPC-задач (наукові обчислення).  
**Використання**: Залежить від навантаження. Наприклад, B1s для студентських проєктів, F для обчислень, E для великих баз даних.

### 2.5. Які дистрибутиви ОС підтримуються у шаблонах в Azure Free Account? Опишіть по одному для сімейства Windows / Linux / Mac.
**Azure Free Account** підтримує:
- **Windows**: Windows Server 2019 Datacenter (750 годин/місяць у Free Tier). Використовується для серверних задач, сумісний із Microsoft-продуктами.
- **Linux**: Ubuntu Server 22.04 LTS. Популярний дистрибутив для вебсерверів, DevOps, контейнерів.
- **Mac**: Azure не підтримує macOS як образ VM через ліцензійні обмеження Apple. Альтернатива – використання Linux/Windows із macOS-емуляторами чи віддаленим доступом до фізичних Mac.

---

## 📋 Хід роботи

### 1. Авторизація в Azure Portal
- Увійшов до Azure Portal ([portal.azure.com](https://portal.azure.com)) за допомогою облікового запису Free Account.
[Скріншот_Відкриття_Azure_Portal](https://github.com/user-attachments/assets/37fa213b-a25b-42ac-9301-f20c3fd34d1b)

1. **Перейдіть на сайт**  
   Відкрийте [azure.microsoft.com/free](https://azure.microsoft.com/free) і натисніть **Try Azure for free**.

2. **Авторизація**  
   Увійдіть за допомогою Microsoft account. Якщо його немає, створіть новий або використайте GitHub account.
![1_PZiRBCVsKiGPWam4rWE3Og](https://github.com/user-attachments/assets/aa5db692-6ea2-4a8a-b95a-6e6f8d753510)

3. **Верифікація карткою**  
   Заповніть форму верифікації картки. Порада: скористайтеся сервісом Revolut, щоб безкоштовно створити міжнародний банківський рахунок і згенерувати віртуальну картку.
![1_N_b5IXkpe72M_EsfQZFlyw](https://github.com/user-attachments/assets/2faa51dc-5152-4866-ba5d-874fc0f565f9)

4. **Підтвердження угоди**  
   Поставте галочку в угоді та натисніть **Sign up**. Ваш Azure account створено!
![1_Hqdz6jMaGG5jurEeAa82rg](https://github.com/user-attachments/assets/9fc44e8e-43ba-42fa-b948-809a49b88390)

5. **Доступ до Azure Portal**  
   Якщо вас не перенаправило до Azure Portal, перейдіть за [посиланням](https://portal.azure.com).

### Практичне завдання №1. Віртуальна машина Linux

#### 2. Створення віртуальної машини Linux
- Перейшов до **Virtual Machines** → **Create** → **Azure virtual machine**.
- Налаштування:
  - **Назва VM**: Linux_Nagornyi_IM_RPZ24B
  - **Region**: (US) East US
  - **Availability options**: No infrastructure redundancy required
  - **Image**: Ubuntu Server 18.04 LTS or 22.04 LTS 
  - **Size**: B1s (Free Tier)
  - **Authentication type**: SSH public key
  - **Inbound ports**: SSH (22), HTTP (80), HTTPS (443)
  - **Disks**: Standard SSD 8 GB
<img width="397" height="94" alt="project-details" src="https://github.com/user-attachments/assets/c30f6497-ed34-4af3-b5f2-331e8e718def" />

<img width="1044" height="452" alt="image" src="https://github.com/user-attachments/assets/85834fb0-82bb-451d-8d7d-0144cc042f4e" />

<img width="525" height="137" alt="administrator-account" src="https://github.com/user-attachments/assets/57898c09-4f57-4517-9551-e138c2cd36a2" />

<img width="796" height="280" alt="inbound-port-rules" src="https://github.com/user-attachments/assets/0572c59b-6957-4d85-a027-cf5032d7cccd" />


#### 3. Налаштування User Data (Cloud-init)
- У розділі **Advanced** → **Custom data** вставлено скрипт:
```bash
#!/bin/bash
apt-get update -y
apt-get install -y nginx
systemctl enable nginx
systemctl start nginx
```

<img width="1023" height="721" alt="cloud-init" src="https://github.com/user-attachments/assets/d83b404f-8e73-4062-bc91-68b767e39fbb" />

- Натиснув **Review + Create** → **Create**.
- Після розгортання знайшов Public IP у властивостях VM.
- Відкрив IP у браузері – побачив стартову сторінку Nginx.
<img width="1365" height="681" alt="499036658-c1e1f492-c6f7-404f-a1bf-70ddb019b112" src="https://github.com/user-attachments/assets/a711dd45-480f-4f54-94a2-252a13dbf72d" />

#### 4. Перевірка через Azure CLI
- Виконав команди:
  ```bash
  az login
  az vm list -d -o table
  ssh -i ~/.ssh/id_rsa azureuser@<Public-IP>
  ```
- Перевірив стан VM та підключився через SSH.
<img width="877" height="631" alt="image" src="https://github.com/user-attachments/assets/9047b871-4c8c-4c04-abfe-3d8418c319fb" />

#### 5. Налаштування Nginx
- Через SSH підключився до VM:
  ```bash
  ~/.ssh/id_rsa azureuser@<Public-IP>
  ```
- Відредагував конфігураційний файл Nginx (`/etc/nginx/sites-available/default`):
  ```bash
  sudo nano /etc/nginx/sites-available/default
  ```
- Додав HTML-сторінку з інформацією про команду:
**Редагований index.html**
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
  <p>If you see this page, the web server is successfully installed and working. Further configuration is required.</p>
  <p>For online documentation and support please refer to <a href="https://nginx.org">nginx.org</a>.<br>
     Commercial support is available at <a href="https://nginx.com">nginx.com</a>.</p>
  <p>Thank you for using Nginx.</p>

  <div class="info">Інформація про команду: РПЗ-24 — Нагорний Ілля</div>
</body>
</html>
```

**Оновлена сторінка**
<img width="1059" height="434" alt="499035481-6a017588-14d8-41b6-b339-74c3e11ef990" src="https://github.com/user-attachments/assets/f77f5bcd-d273-4d1c-a0fc-af91dc9e03df" />

#### 6. Зупинка та видалення VM
- Зупинив VM через Azure Portal: **Virtual Machines** → **Linux_Nagornyi_IM_RPZ24B** → **Stop (deallocate)**.
- Через Azure CLI:
  ```bash
  az vm stop --name Linux_Nagornyi_IM_RPZ24B --resource-group <ResourceGroup_Name>
  ```
- Видалив VM:
  ```bash
  az vm delete --name Linux_Nagornyi_IM_RPZ24B --resource-group <ResourceGroup_Name> --yes
  ```
<img width="965" height="446" alt="image" src="https://github.com/user-attachments/assets/e248782d-7f4c-49a4-89cc-374c63b7538c" />


### Практичне завдання №2. Віртуальна машина Windows Server
<img width="1313" height="760" alt="image" src="https://github.com/user-attachments/assets/4271c554-2a7f-46a4-b123-61b43bc44507" />

#### 7. Створення віртуальної машини Windows
- Перейшов до **Virtual Machines** → **Create** → **Azure virtual machine**.
- Налаштування:
  - **Назва VM**: Windows_Nagornyi_IM_RPZ24B
  - **Region**: West Europe
  - **Image**: Windows Server 2019 Datacenter
  - **Size**: B1s (Free Tier)
  - **Authentication type**: Password
  - **Inbound ports**: RDP (3389)
- Натиснув **Review + Create** → **Create**.
- Після розгортання знайшов Public IP.
<img width="1167" height="551" alt="instance-details" src="https://github.com/user-attachments/assets/3fd93c9b-3738-4e15-908f-e7f881c4ec15" />
<img width="590" height="116" alt="administrator-account" src="https://github.com/user-attachments/assets/fd629d12-bd1b-4083-bb28-e563da965a2a" />
<img width="586" height="210" alt="inbound-port-rules" src="https://github.com/user-attachments/assets/3439a115-0325-49a4-90c2-df9cc9220a82" />
<img width="787" height="268" alt="review-create" src="https://github.com/user-attachments/assets/09d5372c-5bc2-4817-9518-a1df4c5f0e97" />
<img width="973" height="839" alt="validation" src="https://github.com/user-attachments/assets/9188ae25-0307-4190-bf8b-458b44e5b1be" />
<img width="795" height="183" alt="next-steps" src="https://github.com/user-attachments/assets/37b154ab-cd85-4d8a-b175-89cb1a31ac06" />

#### 7. Підключення через RDP та зміна імені сервера
- Запустив Remote Desktop Connection, ввів Public IP.
- Увійшов із логіном та паролем, вказаними при створенні VM.
- Переглянув поточну назву комп’ютера: **This PC** → **Properties**.
- Змінив ім’я сервера:
  - **Settings** → **System** → **About** → **Rename this PC**.
  - Нова назва: WSERVER_Nagornyi_RPZ24B.
  - Перезавантажив VM.
- Повторно підключився через RDP, перевірив зміну імені.
<img width="845" height="199" alt="portal-quick-start-9" src="https://github.com/user-attachments/assets/14c92373-0548-417e-b889-ab1f87f9f8df" />

<img width="830" height="301" alt="image" src="https://github.com/user-attachments/assets/76d6917c-6f59-440d-8dbe-303effa38b45" />

#### 8. Зупинка та видалення VM
- Зупинив VM через Azure Portal: **Virtual Machines** → **Windows_Nagornyi_IM_RPZ24B** → **Stop (deallocate)**.
- Через Azure CLI:
  ```bash
  az vm stop --name Windows_Nagornyi_IM_RPZ24B --resource-group <ResourceGroup_Name>
  ```
- Видалив VM:
  ```bash
  az vm delete --name Windows_Nagornyi_IM_RPZ24B --resource-group <ResourceGroup_Name> --yes
  ```
<img width="965" height="446" alt="comet_sVECszC8gA" src="https://github.com/user-attachments/assets/685af246-a81a-494a-9a7e-12f84893a057" />

---


## ❓ Контрольні питання

1. **Яку роль відіграють SSH-ключі або паролі при підключенні до Azure Virtual Machine?**  
   SSH-ключі (для Linux) або паролі (для Windows/Linux) використовуються для автентифікації при підключенні до VM. SSH-ключі забезпечують безпечний доступ через пару ключів (публічний/приватний), тоді як паролі – простіший, але менш безпечний метод.

2. **Яка команда використовується для підключення до Linux-віртуальної машини в Azure через SSH?**  
   ```bash
   ssh -i ~/.ssh/<key_file> <username>@<Public-IP>
   ```
   Наприклад: `ssh -i ~/.ssh/id_rsa azureuser@20.123.45.67`.

3. **Як ще можна підключитися до Linux-віртуальної машини в Azure?**  
   - Через Azure Bastion (безпечне підключення через браузер).
   - Через Azure Cloud Shell із вбудованим SSH-клієнтом.
   - Через пароль (якщо обрано Authentication type: Password).

4. **Як можна підключитися до Windows-віртуальної машини в Azure?**  
   Через Remote Desktop Protocol (RDP) за допомогою програми Remote Desktop Connection, ввівши Public IP, логін і пароль. Альтернатива – Azure Bastion для браузерного доступу.

5. **У чому відмінність між станами Stop (Deallocate) і Delete для віртуальної машини в Azure?**  
   - **Stop (Deallocate)**: VM зупиняється, ресурси (CPU, RAM) звільняються, але диски та налаштування зберігаються. Не нараховується плата за обчислення, лише за сховище.
   - **Delete**: VM і всі пов’язані ресурси (диски, IP) видаляються, що повністю звільняє ресурси і припиняє нарахування плати.

---

## 📝 Висновки
Лабораторна робота №7 дозволила ознайомитися з процесом створення та управління віртуальними машинами в Azure. Виконано налаштування Linux VM (Ubuntu) із встановленням Nginx та кастомізацією вебсторінки, а також Windows Server VM зі зміною імені сервера. Освоєно підключення через SSH і RDP, управління через Azure CLI та Azure Portal. Робота поглибила розуміння хмарних технологій, зокрема Azure Virtual Machines, Managed Disks, Snapshots і NSG.

---

## 🔗 Корисні посилання
- [Azure Portal](https://portal.azure.com)
- [Azure CLI Documentation](https://docs.microsoft.com/en-us/cli/azure/)
- [Azure Virtual Machines](https://learn.microsoft.com/en-us/azure/virtual-machines/)
- [How to Create a Free Windows Virtual Machine in Azure Portal](https://youtu.be/m8Ed3GBwsTE?si=HnCSXcqeC_sllh-s)
- [How to Create a Linux Virtual Machine in Azure with Ubuntu](https://youtu.be/eLC62_6IxeU?si=R0ZmRT58HbU73voy)
- [Azure список відтворення на 4 відео](https://youtube.com/playlist?list=PL6NQqiVbmsYN0qcpdl-qpIVs_FBphB9-g&si=h01OfWAVqCm-3eiS)
- [Швидкий огляд Azure Virtual Machine](https://youtu.be/cDEKCTCIihM?si=0PDCYqFmX8Mg2dYR)
- [Віртуальні машини в Windows Azure](https://youtu.be/u2D4lXCAqEw?si=nuN4-BPWNAzHksn6)


## 🎯 Система оцінювання
- 📚 Питання попередньої підготовки: 5 балів
- 📋 Практичне завдання №1 (Linux VM): 5 балів
- 📋 Практичне завдання №2 (Windows VM): 5 балів
- ❓ Контрольні питання та висновки: 5 балів
- 🌐 Використання англійської мови (фрагментарно): +5 балів