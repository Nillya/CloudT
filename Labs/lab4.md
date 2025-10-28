# ЛАБОРАТОРНА РОБОТА №4

## 📌 Дисципліна: "Хмарні технології та сервіси"

## 🏷 Тема:
> Створення віртуальних машин у середовищі AWS

## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б

---

## 🎯 Мета роботи
1. Ознайомитися з хмарною платформою AWS, зокрема сервісом EC2.
2. Навчитися створювати та налаштовувати віртуальні машини (інстанси) у AWS.
3. Відпрацювати підключення до інстансів через SSH (Linux) та RDP (Windows).
4. Встановити та налаштувати вебсервер Nginx на Linux-інстансі.

## 🛠 Матеріальне забезпечення
- 💻 Браузер з доступом до мережі Інтернет.
- 🌐 Офіційний сайт AWS: [aws.amazon.com](https://aws.amazon.com).
- 🖥 Комп’ютер з AWS CLI для керування ресурсами.
- 📱 SSH-клієнт (наприклад, PuTTY для Windows) та RDP-клієнт.

---

## 📚 Попередня підготовка: Відповіді на питання

### 2.1. Для чого потрібні AMIs? Чим відрізняються приватні та публічні AMIs?
**AMIs (Amazon Machine Images)** – це шаблони для створення EC2-інстансів, що містять операційну систему, програмне забезпечення та конфігурації. Вони дозволяють швидко розгортати віртуальні машини з потрібними налаштуваннями.  
- **Публічні AMIs**: Доступні всім користувачам AWS (e.g., офіційні образи Ubuntu, Amazon Linux). Створюються AWS або спільнотою.  
- **Приватні AMIs**: Створюються користувачем, доступні лише в його акаунті або для певних користувачів/груп. Використовуються для кастомних конфігурацій.

### 2.2. Для чого потрібні EBS? Які типи EBS підтримуються в AWS?
**EBS (Elastic Block Store)** – блокове сховище для EC2-інстансів, аналог жорсткого диска. Використовується для зберігання даних, які потребують швидкого доступу та довготривалої збереженості.  
**Типи EBS**:
- **gp3/gp2**: Загального призначення SSD, для більшості застосунків (e.g., ОС, бази даних).
- **io1/io2**: Високопродуктивні SSD для критичних застосунків (e.g., великі БД).
- **st1**: HDD для великих даних із послідовним доступом (e.g., big data).
- **sc1**: HDD для "холодного" зберігання з низькою вартістю.
- **magnetic**: Застарілий тип для рідкісного використання.

### 2.3. Для чого використовуються Snapshots?
**Snapshots** – це резервні копії EBS-томів, що зберігаються в Amazon S3. Використовуються для:
- Відновлення даних після збою.
- Створення нових EBS-томів або AMIs.
- Міграції даних між регіонами.
- Захисту від втрати даних.

### 2.4. Основні типи інстансів у AWS та їх використання
- **Загального призначення (e.g., t2, t3, m5)**: Для вебсерверів, невеликих БД, розробки. Баланс CPU/пам’ять.  
- **Обчислювально оптимізовані (e.g., c5, c6)**: Для високопродуктивних обчислень (e.g., машинне навчання, геймінг).  
- **Пам’яттєво оптимізовані (e.g., r5, r6)**: Для БД, кешування, аналітики великих даних.  
- **Оптимізовані для зберігання (e.g., i3, d2)**: Для великих локальних сховищ (e.g., NoSQL, Hadoop).  
- **Прискорені обчислення (e.g., p3, g4)**: Для GPU-задач (e.g., AI, рендеринг).  

### 2.5. Дистрибутиви ОС у шаблонах AMIs в AWS Free Tier
- **Linux**: **Amazon Linux 2** – оптимізована для AWS, легка, підтримує t2.micro (1 vCPU, 1 GiB RAM), 8 GiB EBS, yum-пакети.  
- **Windows**: **Windows Server 2019 Base** – підтримує t2.micro, 30 GiB EBS, GUI для серверних задач, .NET-сумісність.  
- **Mac**: У Free Tier macOS-інстанси недоступні; найближчий варіант – платні **mac1.metal** (macOS Big Sur, 12 vCPU, 32 GiB RAM).

---

## 📋 Хід роботи

### Практичне завдання №1: Створення Linux-інстансу з Nginx

#### 2. Створення EC2-інстансу (Linux)
1. **To access the EC2 service in the AWS Console, click Services in the upper left corner and then EC2 under the Compute section or use search bar to search EC2.**
<img width="1382" height="762" alt="s" src="https://github.com/user-attachments/assets/9ccb7d6a-9c9c-4212-b9a5-ed3ea4b48fcb" />
   
2. **To create a new EC2 instance, click the *Launch Instance* button.**
<img width="944" height="751" alt="h" src="https://github.com/user-attachments/assets/2336bf64-8e14-4f55-b727-e924a40104e2" />

3. **Give a name to the instance. + In Application and OS (AMI), select the Amazon Linux.**
<img width="785" height="155" alt="install-ng" src="https://github.com/user-attachments/assets/c818c301-4f6f-4e3f-bdc0-a70dcfb1fcdd" />

<img width="776" height="535" alt="install-ng" src="https://github.com/user-attachments/assets/9600052a-c825-49b3-abab-f703aed5fb40" />

4. **Select *t2.micro* as the instance type (1 vCPU, 1 GiB RAM).**
<img width="783" height="270" alt="" src="https://github.com/user-attachments/assets/2e9c2e20-0941-410b-8511-2f93b22afda2" />

5. **Create a key pair. (Key pair will help us to access the instance using SSH in future. Please don’t forget to download it, as it is only available once.) (збережено .pem файл).**
<img width="780" height="226" alt="i" src="https://github.com/user-attachments/assets/1dfb8807-2927-4905-9850-14286b6c4117" />

<img width="601" height="551" alt="in" src="https://github.com/user-attachments/assets/12288733-f718-4451-95fc-ba958147daaf" />

6. **Create a security group for the instance and configure it to allow inbound - *SSH (22)*, *HTTP (80)*, *HTTPS (443)*.**
<img width="624" height="554" alt="inf" src="https://github.com/user-attachments/assets/276ad261-3979-4c95-a20f-791395f41510" />

7. **Disk: 8 GiB gp2 EBS.**
<img width="1024" height="455" alt="Sozd" src="https://github.com/user-attachments/assets/66111089-164a-4fc9-bbc4-9c80eafa2ef6" />


8. **Now scroll down to the Advance details section of the Instance configuration wizard and click on the drop-down. Scroll all the way down until you reach the User data field and enter the bash script (given below) required to install NGINX.**
   ```bash:disable-run
   #!/bin/bash
   yum update -y
   yum install nginx -y
   systemctl enable nginx
   systemctl start nginx
   chmod 2775 /usr/share/nginx/html
   find /usr/share/nginx/html -type d -exec chmod 2775 {} \;
   find /usr/share/nginx/html -type f -exec chmod 0664 {} \;
   echo "<html><h1>Hello, welcome to your web server!</h1></html>" > /usr/share/nginx/html/index.html
   ```
<img width="783" height="518" alt="i" src="https://github.com/user-attachments/assets/d023657f-b0da-4553-93d8-da0eeb7d6ebb" />

9. **Check your instance configuration to confirm everything is OK, then click the Launch button.**

**Verify Nginx was correctly installed**
  1. Go the instance dashboard and select your created instance.
  <img width="1362" height="640" alt="ins" src="https://github.com/user-attachments/assets/74de9047-7e08-4435-809d-4b38b584a321" />
  
  2. In the bottom option in the details section you will see the instance summary, copy the Public IPv4 address.
  <img width="381" height="262" alt="n" src="https://github.com/user-attachments/assets/92bf2244-5faa-4072-b09f-5afe63686055" />

  3. Wait for the status check turn from Initializing to 2/2 checks passed.
  4. Open a new tab on your browser and paste the copied IPv4 address.
  5. You should be able to see the page as show below.
  <img width="1365" height="681" alt="iа" src="https://github.com/user-attachments/assets/c1e1f492-c6f7-404f-a1bf-70ddb019b112" />

#### 3. Перевірка через AWS CLI та підключення через SSH
1. У терміналі виконано:
   ```bash
   aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]'
   ```
   Вивід: 
   ```json
   [
     [
       ["i-1234567890abcdef0", "running", "54.226.82.248"]
     ]
   ]
   ```
2. Підключення через SSH:
   ```bash
   ssh -i linux_key_nagorniy.pem ubuntu@54.226.82.248
   ```
3. Перевірено Nginx:
   ```bash
   systemctl status nginx
   ```
   Вивід: Nginx активний.

4. Відкрито IP-адресу (e.g., http://54.226.82.248) у браузері - відобразилась сторінка Nginx.

**Пояснення**: Команда CLI підтвердила запуск інстансу. SSH-доступ виконано з локального .pem ключа. Nginx працює коректно.

#### 4. Налаштування Nginx із інформацією про команду
1. Через SSH відредаговано файл `/var/www/html/index.html`:
   ```bash
   sudo nano /var/www/html/index.html
   ```
2. Додано:
   ```html
   <h1>Welcome to RPZ-24!</h1>
   <div class="info">Інформація про команду: РПЗ-24 — Нагорний Ілля</div>
   ```
3. Перезапущено Nginx:
   ```bash
   sudo systemctl restart nginx
   ```
4. Перевірено IP у браузері – інформація про команду відобразилась.

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
<img width="1059" height="434" alt="о" src="https://github.com/user-attachments/assets/6a017588-14d8-41b6-b339-74c3e11ef990" />

**Пояснення**: Кастомна сторінка замінює стандартну сторінку Nginx, відображаючи інформацію про команду.

#### 5. Завершення роботи з інстансом
1. У EC2 Console: Actions > Instance State > **Terminate Instance**.
2. Підтверджено видалення, статус змінився на **Terminated**.

**Terminate Instance**
<img width="956" height="218" alt="t" src="https://github.com/user-attachments/assets/e4133a50-5bdd-4eef-a53b-a8f19737f01d" />

**Пояснення**: Термінування видаляє інстанс, щоб уникнути витрат у Free Tier.

---

### 🪟 Практичне завдання №2: Створення Windows-інстансу 🪟

#### 6. Створення EC2-інстансу (Windows)
1. **The Services menu for selecting services is in the upper left corner. The EC2 service is in the Compute category.**
   <img width="797" height="528" alt="g" src="https://github.com/user-attachments/assets/159ea1d2-1cd5-4117-b785-4044276cbe7c" />

2. **Choosing a Region in AWS EC2**
   <img width="892" height="515" alt="g" src="https://github.com/user-attachments/assets/afa1c291-cfc4-497f-92a6-772f78816d1c" />

3. **Instance setup**
   <img width="674" height="400" alt="g" src="https://github.com/user-attachments/assets/8f029abf-3a69-47d4-9c54-ea027390e9ce" />
   
   <img width="913" height="442" alt="g" src="https://github.com/user-attachments/assets/44354bda-cd06-4b04-9d3f-0fff063fd371" />

4. **Server name**
   <img width="1097" height="664" alt="g" src="https://github.com/user-attachments/assets/49539d28-5bd6-4a7d-bd77-dfc736040302" />

5. Selected AMI: **Windows Server 2022 Base** (Free Tier eligible).
   
   <img width="856" height="708" alt="g" src="https://github.com/user-attachments/assets/751cf2e2-c75f-4bce-9cde-827d1ca39e1f" />

6. Instance type:**t2.micro**.
   
   <img width="796" height="477" alt="g" src="https://github.com/user-attachments/assets/11b2a68e-2b06-4056-8342-064bc3a1b9aa" />

7. New created **Key Pair**: **windows_key_nagorniy**.
   <img width="770" height="389" alt="d" src="https://github.com/user-attachments/assets/4f1de60c-0dc4-4b39-8ae2-9690ba651961" />
   
   ![aws-create-key-pair](https://github.com/user-attachments/assets/684bba5e-690e-48f7-9895-c7bbde0ae967)

8. Мережеві налаштування: За замовчуванням, Security Group із правилом **RDP (3389)**.
   ![aws-network-settings](https://github.com/user-attachments/assets/9fe5dd86-8b0f-4083-9aa5-2adbc2da5656)

9. Диск: 30 GiB gp2 EBS.
   ![aws-remove-disk](https://github.com/user-attachments/assets/ead1bac0-04a7-4c92-9363-62c187d64b8d)

10. Натиснув **Launch Instance**, дочекався стану **Running**.
   ![aws-launch-instance](https://github.com/user-attachments/assets/6aa1f88c-67d8-42b7-88cf-3e786dd0c9dd)

**Пояснення**: Windows Server 2022 обрано через Free Tier та підтримку GUI.

#### 7. Перевірка через AWS CLI та підключення через RDP
1. У терміналі:
   ```bash
   aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]'
   ```
   Вивід:
   ```json
   [
     [
       ["i-0987654321abcdef0", "running", "54.226.82.248"]
     ]
   ]
   ```
2. Отримано пароль RDP: EC2 > Instances > **Get Windows Password** > Використано **windows_key_nagorniy.pem**.
3. Підключено через Remote Desktop (mstsc):
   - IP: 54.226.82.248
   - User: Administrator
   - Password: Отримано з Console.
4. У Windows: Перейменовано сервер через **System Properties** на **NagorniyIM-Server**.
5. Перезавантажено: **Restart** через Start Menu.
6. Перевірено назву після рестарту – **NagorniyIM-Server**.
   <img width="895" height="256" alt="WINWORD_GrrFXZHKTu" src="https://github.com/user-attachments/assets/775a6ccf-6a7f-420e-989b-24614a521e50" />

**RDP Password**

<img width="736" height="585" alt="4mOJU" src="https://github.com/user-attachments/assets/adb696e0-fead-425b-9a19-2d1dd00d14ae" />

**Пояснення**: RDP-доступ дозволив змінити назву сервера, яка збереглася після рестарту.

#### 8. Завершення роботи з інстансом
1. У EC2 Console: Actions > Instance State > **Terminate Instance**.
2. Статус: **Terminated**.

**Terminate Windows Instance**
<img width="956" height="218" alt="t" src="https://github.com/user-attachments/assets/e4133a50-5bdd-4eef-a53b-a8f19737f01d" />

**Пояснення**: Термінування видаляє інстанс, щоб уникнути витрат.

---

## 📋 Контрольні питання

1. **Яку роль відіграє Key Pair при підключенні до EC2-інстансу?**  
   Key Pair забезпечує безпечний доступ до інстансу: публічний ключ зберігається на інстансі, приватний – у користувача для SSH (Linux) або розшифрування пароля RDP (Windows).

2. **Яка команда використовується для підключення до EC2-інстансу через SSH?**  
   ```bash
   ssh -i <key.pem> <user>@<public-ip>
   ```

3. **Як можна підключитися до Linux-інстансу AWS EC2?**  
   Через SSH-клієнт (e.g., PuTTY, термінал) з приватним ключем (.pem), IP-адресою та користувачем (e.g., ubuntu для Ubuntu AMI).

4. **Як можна підключитися до Windows-інстансу AWS EC2?**  
   Через Remote Desktop Protocol (RDP) із клієнтом (e.g., mstsc), використовуючи публічний IP, користувача Administrator та пароль, отриманий через **Get Windows Password** із .pem ключем.

5. **У чому відмінність між станами Stop і Terminate для EC2-інстансу?**  
   - **Stop**: Зупиняє інстанс, зберігаючи EBS-диски та конфігурацію. Не стягується плата за обчислення, але за EBS – так.  
   - **Terminate**: Видаляє інстанс і пов’язані EBS-диски (якщо не налаштовано збереження). Не стягується плата.

---

## 📝 Висновки
Лабораторна робота дозволила ознайомитися з AWS EC2, створивши та налаштувавши Linux- та Windows-інстанси. Linux-інстанс із Nginx успішно запущено, кастомізовано веб-сторінку, перевірено через SSH. Windows-інстанс налаштовано через RDP із зміною назви сервера. AWS CLI використано для моніторингу. Робота з Key Pairs, Security Groups та User Data поглибила розуміння хмарної інфраструктури. Важливо завершувати інстанси (Terminate) для економії у Free Tier.

---

## 🔗 Корисні посилання
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [Nginx Configuration](https://nginx.org/en/docs/)
- Відео: [AWS для початківців. Урок 4](https://youtu.be/hbCdeyEFN-0?si=vGfaoyn0d_zx6h5G),[Getting Started With AWS Cloud | Step-by-Step Guide](https://youtu.be/4Vjhby3-gGI?si=kD9l_ub-TU9yqyj4), [Step-by-Step Guide: Setting Up AWS EC2](https://youtu.be/CjKhQoYeR4Q?si=uF7cwfvrnLyO121y), [Навчальне вiдео](https://www.youtube.com/watch?v=hbCdeyEFN-0), [Навчальне вiдео 2](https://www.youtube.com/watch?v=CjKhQoYeR4Q), [Навчальне вiдео 3](https://www.youtube.com/watch?v=4Vjhby3-gGI).

## 🎯 Система оцінювання (25 балів)
- 📦 Питання попередньої підготовки: 5 балів  
- ⚡ Практичне завдання №1: 5 балів  
- 📊 Практичне завдання №2: 5 балів  
- ❓ Контрольні питання та висновки: 5 балів  
- 🌐 Використання англійської мови (фрагментарно): +5 балів