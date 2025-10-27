# 📋 ЛАБОРАТОРНА РОБОТА №8

## 📌 Дисципліна: "Хмарні технології та сервіси"

## 🏷 Тема:
> Реєстрація та знайомство з хмарним середовищем Google Cloud Platform

## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б

---

## 🎯 Мета роботи
1. Ознайомитися з хмарним провайдером Google Cloud Platform (GCP), зокрема з його основними сервісами та інтерфейсом.
2. Зареєструвати акаунт Free Trial у GCP та налаштувати базові функції безпеки.
3. Освоїти використання Google Cloud Console та Cloud SDK (CLI) для керування ресурсами.
4. Виконати практичні завдання з налаштування груп, бюджетів та перевірки ресурсів.

## 🛠 Матеріальне забезпечення
- 💻 Браузер з доступом до мережі Інтернет.
- 🌐 Сайт Google Cloud Platform: [cloud.google.com](https://cloud.google.com).
- Google Cloud SDK (CLI) для виконання команд.
- Google Authenticator або SMS для двофакторної аутентифікації.

---

## 📚 Попередня підготовка: Відповіді на питання
### 2.1. Що таке віртуальна машина та які особливості їх реалізації у Google Compute Engine?
**Віртуальна машина (VM)** – це ізольоване програмне середовище, яке емулює фізичний комп’ютер, дозволяючи запускати операційні системи та додатки на хмарній інфраструктурі. У **Google Compute Engine** VM працюють на базі дата-центрів Google із такими особливостями:
- **Масштабування**: Підтримка автоматичного масштабування для адаптації до навантаження.
- **Типи машин**: Різні конфігурації (загального призначення, оптимізовані для CPU, пам’яті чи GPU).
- **Preemptible VMs**: Дешевші, але тимчасові машини для некритичних задач.
- **Live Migration**: Безперервна робота VM під час оновлень апаратного забезпечення.
- **Кастомізація**: Можливість створювати власні образи та налаштовувати диски.

### 2.2. Які можливості надає Google App Engine для розгортання веб-застосунків?
**Google App Engine** – платформа для розгортання веб-додатків без необхідності керувати серверами. Основні можливості:
- **Автоматичне масштабування**: Динамічне виділення ресурсів залежно від трафіку.
- **Підтримка мов**: Python, Java, Node.js, PHP, Ruby, Go тощо.
- **Управління версіями**: Розгортання різних версій додатка для тестування чи оновлень.
- **Інтеграція**: Легке підключення до Google Cloud Storage, Cloud SQL, BigQuery.
- **Безсерверна архітектура**: Розробники зосереджуються на коді, а не на інфраструктурі.

### 2.3. Які основні кроки створення App Engine-додатка через Google Cloud Console?
1. Увійти до Google Cloud Console ([console.cloud.google.com](https://console.cloud.google.com)).
2. Створити новий проєкт або обрати існуючий.
3. Увімкнути API для App Engine у розділі **APIs & Services**.
4. Перейти до **App Engine** → **Create Application**.
5. Вибрати регіон (наприклад, europe-west).
6. Налаштувати середовище (Standard або Flexible).
7. Завантажити код додатка через Cloud SDK (`gcloud app deploy app.yaml`).
8. Перевірити розгортання, відкривши URL додатка.

### 2.4. Які особливості реалізації Identity and Access Management (IAM) у GCP?
**Cloud IAM** керує доступом до ресурсів GCP через ролі та політики:
- **Ролі**: Набори дозволів (наприклад, Viewer, Editor, Owner).
- **Гнучкість**: Можливість призначати ролі на рівні проєкту, ресурсу чи організації.
- **Service Accounts**: Спеціальні акаунти для програмного доступу до ресурсів.
- **Принцип найменших привілеїв**: Обмеження доступу до необхідного мінімуму.
- **Аудит**: Логи доступу через Cloud Audit Logs.

### 2.5. Розкрийте використання версій (Versions) у App Engine для управління оновленнями додатків.
У **App Engine** версії дозволяють:
- Розгортати різні версії одного додатка паралельно (наприклад, для A/B тестування).
- Перемикати трафік між версіями через Google Cloud Console.
- Відкат до попередньої версії у разі помилок.
- Керувати конфігураціями через `app.yaml` для кожної версії.
- Видаляти застарілі версії для економії ресурсів.

### 2.6. Здійсніть огляд Cloud Storage та його ключових функцій.
**Cloud Storage** – об’єктне сховище для зберігання файлів. Ключові функції:
- **Масштабність**: Необмежений обсяг даних без ручного керування.
- **Доступність**: 99.9% SLA для Standard класу.
- **Життєвий цикл**: Автоматичне переміщення об’єктів між класами сховища.
- **Версіонування**: Збереження попередніх версій файлів.
- **Доступ**: Через HTTP/HTTPS, SDK, gsutil чи API.

### 2.7. Охарактеризуйте різні класи сховищ у GCP: Standard, Nearline, Coldline, Archive.
- **Standard**: Для часто використовуваних даних (веб-контент, активні проєкти). Висока швидкість, вища вартість.
- **Nearline**: Для даних із рідкісним доступом (бекапи). Дешевше, але з платою за доступ.
- **Coldline**: Для архівних даних із дуже рідкісним доступом (довгострокові бекапи). Ще нижча ціна.
- **Archive**: Для даних, що зберігаються роками (юридичні архіви). Найдешевший, але з високою вартістю вилучення.

### 2.8. Опишіть, як працювати з Cloud Storage на прикладі використання мови Python.
Використовуємо бібліотеку `google-cloud-storage`:
```python
from google.cloud import storage

# Ініціалізація клієнта
client = storage.Client()

# Створення bucket
bucket_name = "my-unique-bucket"
bucket = client.create_bucket(bucket_name)

# Завантаження файлу
blob = bucket.blob("example.txt")
blob.upload_from_filename("local_file.txt")
print(f"File uploaded to {bucket_name}/example.txt")

# Завантаження файлу з bucket
blob.download_to_filename("downloaded_file.txt")
print("File downloaded")
```
**Пояснення**: Код ініціалізує клієнт, створює bucket, завантажує файл із локального диска та завантажує його назад. Потрібно налаштувати автентифікацію через Service Account.

### 2.9. Що таке Serverless та особливості його реалізації у Cloud Functions і Cloud Run?
**Serverless** – модель, де розробник не керує серверами, а платить лише за виконані обчислення. У GCP:
- **Cloud Functions**: Безсерверне виконання коду у відповідь на події (HTTP-запити, зміни у Cloud Storage). Підходить для легких, подієво-орієнтованих задач.
- **Cloud Run**: Безсерверна платформа для контейнерів. Дозволяє запускати контейнеризовані додатки з автоматичним масштабуванням. Підходить для складніших застосунків.

### 2.10. Поясніть різницю між автентифікацією та авторизацією. Як поняття IAM Roles і Service Accounts у GCP пов’язані з цими процесами?
- **Автентифікація**: Перевірка ідентичності користувача чи сервісу (наприклад, логін через Google Account).
- **Авторизація**: Визначення, які дії дозволені ідентифікованому суб’єкту.
- **IAM Roles**: Набори дозволів, що визначають, які дії може виконувати користувач чи сервіс (авторизація).
- **Service Accounts**: Акаунти для програмного доступу до ресурсів. Використовуються для автентифікації додатків у GCP.

---
## 📋 Хід роботи
### 1. Реєстрація акаунту Free Trial у Google Cloud Platform
1. Перейшов на сайт [cloud.google.com](https://cloud.google.com) і натиснув **Get started for free**.
2. Увійшов за допомогою Google Account.
3. Заповнив форму реєстрації (персональні дані заблюрені), додав картку для верифікації.
4. Отримав підтвердження про 300 USD кредитів на 90 днів.
<img width="2560" height="1248" alt="изображение" src="https://github.com/user-attachments/assets/1fcd269d-364e-49e5-a954-61f7f27927e9" />
<img width="1284" height="856" alt="изображение" src="https://github.com/user-attachments/assets/3b91f8b6-8f2a-4497-8acd-ea9d65e42cd2" />
<img width="1273" height="1166" alt="изображение" src="https://github.com/user-attachments/assets/34c699da-0b1e-4c8b-b861-c969962cc61f" />


### 2. Вхід у Google Cloud Console
1. Перейшов за адресою [console.cloud.google.com](https://console.cloud.google.com).
2. Ознайомився з інтерфейсом:
   - **Dashboard**: Загальний огляд проєктів, ресурсів, активності.
   - **Navigation Menu**: Доступ до всіх сервісів (Compute Engine, Cloud Storage тощо).
   - **Billing**: Інформація про витрати та кредити.
<img width="1896" height="395" alt="изображение" src="https://github.com/user-attachments/assets/7595cf76-578d-44bf-ab17-2d3c6ca68807" />
<img width="450" height="842" alt="изображение" src="https://github.com/user-attachments/assets/3da213d6-56ad-4448-a0f5-a1c6934f1650" />


### 3. Налаштування двофакторної аутентифікації (2-Step Verification)
1. Перейшов у налаштування Google Account → **Security** → **2-Step Verification**.
2. Увімкнув MFA через Google Authenticator.
3. Згенерував QR-код, просканував його у додатку Google Authenticator.
4. Зберіг резервні коди.
<img width="1642" height="801" alt="изображение" src="https://github.com/user-attachments/assets/f96afe48-3917-48fb-9ff4-b29a9bfc03cc" />

<img width="1034" height="582" alt="изображение" src="https://github.com/user-attachments/assets/2ce40c73-3b61-4b84-96e0-e68acd8b7f34" />


### 4. Створення бюджету “Zero Spend Budget”
1. У Google Cloud Console перейшов до **Billing** → **Budgets & alerts**.
2. Створив бюджет із назвою “Zero Spend Budget”, встановив ліміт 0 USD.
3. Налаштував сповіщення на email при досягненні ліміту.

<img width="1174" height="436" alt="изображение" src="https://github.com/user-attachments/assets/7c5ab4e3-4a1e-40a9-b3ad-14ae361961f2" />

<img width="931" height="273" alt="изображение" src="https://github.com/user-attachments/assets/28c35b88-1db5-4ee8-a1ef-8195ca316be1" />

<img width="891" height="394" alt="изображение" src="https://github.com/user-attachments/assets/ab2a7631-8719-4f0b-8c5c-7c496d4ddf0d" />

<img width="795" height="304" alt="изображение" src="https://github.com/user-attachments/assets/b6c7a972-3278-4c84-9cd1-3376fc15f189" />

<img width="235" height="395" alt="изображение" src="https://github.com/user-attachments/assets/d5e5eef0-d9a7-4b30-8242-b7e9dd439085" />

<img width="952" height="353" alt="изображение" src="https://github.com/user-attachments/assets/c2be1f50-8eb5-4a5d-b076-a3e54de301b8" />

<img width="722" height="546" alt="изображение" src="https://github.com/user-attachments/assets/d1c3e72c-d271-4783-91f9-77bcdfb3c60a" />

<img width="721" height="545" alt="изображение" src="https://github.com/user-attachments/assets/18e284fd-db21-401d-a88e-e3c5ac79e798" />

<img width="745" height="475" alt="изображение" src="https://github.com/user-attachments/assets/173595fb-760a-40f9-99c1-e84ee58ef301" />

<img width="735" height="539" alt="изображение" src="https://github.com/user-attachments/assets/813b760c-647c-45ce-887a-822165adcf88" />

<img width="1066" height="385" alt="изображение" src="https://github.com/user-attachments/assets/44d572e2-5730-4e62-81c0-15122a4b25b0" />



### 5. Створення групи та користувачів у Google Cloud IAM
1. У розділі **IAM & Admin** → **Groups** створив групу “developers”.
2. Додав себе (gmail). 
3. Підтвердив створення групи.

<img width="1596" height="761" alt="изображение" src="https://github.com/user-attachments/assets/52ad9dc5-783c-4153-9bde-300c52b00dcb" />

### 6. Створення групи “readonly”
1. У **IAM & Admin** → **Groups** створив групу “readonly”.
2. Додав одного користувача з групи “developers”.
3. Перевірив членство користувача у групах через **IAM & Admin** → **IAM**.

<img width="655" height="581" alt="изображение" src="https://github.com/user-attachments/assets/79e58b71-71f2-4b56-83d8-daad5e07b248" />


### 7. Встановлення Google Cloud SDK (CLI)
1. Завантажив Google Cloud SDK із [cloud.google.com/sdk](https://cloud.google.com/sdk).
2. Встановив на ПК (Windows/Linux/MacOS).
3. Перевірив встановлення командою:
   ```bash
   gcloud --version
   ```
<img width="1161" height="748" alt="изображение" src="https://github.com/user-attachments/assets/c01d1308-0812-4fb4-bf5c-f485702f6c3d" />

<img width="424" height="224" alt="изображение" src="https://github.com/user-attachments/assets/0c4b2f10-c4a0-48a7-90c4-6db251b6dcde" />


### 8. Конфігурація Google Cloud CLI
1. Виконав команду:
   ```bash
   gcloud auth login
   ```
2. Відкрив посилання у браузері, увійшов у Google Account.
3. Підтвердив авторизацію.

<img width="876" height="240" alt="изображение" src="https://github.com/user-attachments/assets/9d6a29b4-ed10-444f-8a35-eda52d15c81b" />


### 9. Перевірка віртуальних машин у Compute Engine
1. Виконав команду:
   ```bash
   gcloud compute instances list
   ```
2. Отримав список (у моєму випадку – порожній, оскільки VM не створено).

<img width="617" height="417" alt="image-221" src="https://github.com/user-attachments/assets/7a0974c9-c8f1-43b6-8c8d-2a0fb699c9fb" />


### 10. Довідковий центр Google Cloud CLI
Створив файл-довідку українською мовою з базовими командами gcloud:

# Довідка з базових команд Google Cloud SDK (gcloud)

1. **Авторизація**
   ```bash
   gcloud auth login
   ```
   Відкриває браузер для авторизації у Google Cloud.

2. **Створення проєкту**
   ```bash
   gcloud projects create my-lab-project --name="My Lab Project"
   ```
   Створює новий проєкт із заданим ID та назвою.

3. **Перегляд проєктів**
   ```bash
   gcloud projects list
   ```
   Показує список усіх доступних проєктів.

4. **Перегляд віртуальних машин**
   ```bash
   gcloud compute instances list
   ```
   Виводить список VM у поточному проєкті.

5. **Створення віртуальної машини**
   ```bash
   gcloud compute instances create my-vm --zone=europe-west1-b --machine-type=e2-micro
   ```
   Створює VM у вказаній зоні з типом машини e2-micro.

6. **Керування ресурсами**
   ```bash
   gcloud compute instances delete my-vm --zone=europe-west1-b
   ```
   Видаляє VM із зазначеної зони.

---
## ❓ Контрольні питання
1. **У чому полягає принцип роботи TOTP-аутентифікації? Наведіть приклади в контексті Google Authenticator і 2-Step Verification.**
   **TOTP (Time-based One-Time Password)** генерує тимчасові паролі на основі часу та секретного ключа. Google Authenticator створює 6-8-значний код кожні 30 секунд. У 2-Step Verification користувач сканує QR-код для прив’язки пристрою, після чого вводить код із Authenticator для підтвердження входу.

2. **Опишіть формат JSON: де він використовується, які його особливості. Чи застосовується цей формат у GCP?**
   **JSON (JavaScript Object Notation)** – легкий формат обміну даними, що використовує пари ключ-значення. Особливості: читабельність, підтримка вкладених структур, широка сумісність. У GCP JSON використовується для:
   - Налаштування ресурсів (наприклад, `app.yaml` в App Engine).
   - API-запитів (Cloud Storage, BigQuery).
   - Логів та конфігурацій.

3. **Які основні API надає Google Cloud Platform? Коротко охарактеризуйте їх призначення.**
   - **Compute Engine API**: Керування VM (створення, запуск, видалення).
   - **Cloud Storage API**: Робота з об’єктним сховищем (завантаження, видалення файлів).
   - **BigQuery API**: Виконання аналітичних запитів до великих даних.
   - **Cloud Functions API**: Розгортання та виклик безсерверних функцій.
   - **IAM API**: Керування доступом і ролями.

4. **Як можна встановити Google Cloud SDK (CLI) під різними операційними системами?**
   - **Windows**: Завантажити інсталятор із [cloud.google.com/sdk](https://cloud.google.com/sdk), запустити, слідувати інструкціям.
   - **Linux**: Додати репозиторій Google Cloud, встановити через `apt` або `yum`.
   - **MacOS**: Завантажити архів, розпакувати, додати `gcloud` до PATH.
   Після встановлення виконати `gcloud init` для ініціалізації.

5. **Розгляньте базові команди gcloud CLI. Наведіть приклади з поясненнями.**
   - `gcloud auth login` – авторизація у Google Cloud.
   - `gcloud projects create my-project` – створення проєкту.
   - `gcloud compute instances list` – перегляд VM.
   - `gcloud app deploy app.yaml` – розгортання додатка в App Engine.
   - `gcloud storage cp file.txt gs://my-bucket` – копіювання файлу до Cloud Storage.

---
## 📝 Висновки
Лабораторна робота №8 дозволила ознайомитися з Google Cloud Platform, її основними сервісами та інструментами. Виконано реєстрацію акаунту Free Trial, налаштування двофакторної аутентифікації, створення бюджету та груп у IAM, встановлення та конфігурація Google Cloud SDK. Робота поглибила розуміння хмарних технологій, зокрема Compute Engine, Cloud Storage, App Engine та IAM. Освоєно базові команди gcloud для керування ресурсами.

---
## 🔗 Корисні посилання
- [Google Cloud Console](https://console.cloud.google.com)
- [Google Cloud SDK Documentation](https://cloud.google.com/sdk/docs)
- [What is Google Cloud Platform?](https://youtu.be/KurQlPvNQ0k?si=8-HSWfdpGA-H1PKY)
- [Google Cloud Platform Tutorials | Edureka](https://youtube.com/playlist?list=PL9ooVrP1hQOFUm7TmkH1zk5xy75GAxV44&si=6bTmTYC3X0-BLJlZ)
- [Google Cloud Skills Boost](https://www.cloudskillsboost.google)
- [Google Cloud SDK](https://cloud.google.com/sdk/docs/install)

## 🎯 Система оцінювання
- 📚 Питання попередньої підготовки: 5 балів
- 📋 Практичні завдання: 10 балів
- ❓ Контрольні питання та висновки: 5 балів
- 🌐 Використання англійської мови (фрагментарно): +5 балів