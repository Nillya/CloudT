# ЛАБОРАТОРНА РОБОТА №3

## 📌 Дисципліна: "Хмарні технології та сервіси"

## 🏷 Тема:
> Реєстрація та знайомство з хмарним середовищем AWS

## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б

---

## 🎯 Мета роботи
1. Зареєструвати акаунт у AWS Free Tier та ознайомитися з інтерфейсом AWS Management Console.
2. Налаштувати базові інструменти безпеки (MFA, IAM) та моніторингу (Budgets).
3. Встановити та налаштувати AWS CLI для керування ресурсами.

## 🛠 Матеріальне забезпечення
- 💻 Браузер FireFox з доступом до мережі Інтернет.
- 📱 Смартфон з додатком для MFA (наприклад, Google Authenticator).
- 🖥️ Комп'ютер з Windows/MacOS для встановлення AWS CLI.
- 🌐 Офіційний сайт AWS: [aws.amazon.com](https://aws.amazon.com).

---

## 📚 Короткі теоретичні відомості
Amazon Web Services (AWS) – провідна хмарна платформа, що надає доступ до обчислювальних ресурсів через інтернет. AWS дозволяє уникати витрат на фізичну інфраструктуру, пропонуючи масштабовані рішення для бізнесу та розробників. Основні компоненти:
- **Регіони (Regions)** та **Зони доступності (Availability Zones)**: Забезпечують відмовостійкість і низьку затримку.
- **Сервіси**:
  - **Обчислення**: EC2 (віртуальні сервери), Lambda (serverless).
  - **Зберігання**: S3 (об'єктне), EBS (блокове).
  - **Бази даних**: RDS (реляційні), DynamoDB (NoSQL).
  - **Мережа**: VPC (віртуальні мережі), Route 53 (DNS).
  - **Безпека**: IAM (керування доступом), CloudWatch (моніторинг).

AWS Free Tier надає 12 місяців безкоштовного доступу до ключових сервісів (наприклад, 750 годин EC2 t2.micro/місяць). Реєстрація вимагає email, пароля та платіжних даних для верифікації. AWS Management Console – веб-інтерфейс для керування. IAM керує користувачами, групами, ролями та політиками (JSON-формати). MFA додає двофакторну автентифікацію. AWS CLI – інструмент для командного рядка, налаштовується через `aws configure`.

---

## 📋 Попередня підготовка: Відповіді на питання з відео

### 2.1. Основні поняття та терміни з першого відео (AWS для початківців: Урок 1)
Згідно з уроком 1, ключові поняття: **Глобальна інфраструктура** (regions – географічні локації, AZ – зони в регіоні для відмовостійкості), **основні сервіси** (EC2 для VM, S3 для storage, Lambda для serverless), **вартість** (pay-as-you-go модель, Free Tier). Категорії сервісів: Compute (EC2, Lambda), Storage (S3, EBS), Database (RDS, DynamoDB), Networking (VPC, Route 53), Security (IAM, CloudWatch).

### 2.2. MFA в AWS (з другого відео)
MFA (Multi-Factor Authentication) потрібна для захисту акаунту від несанкціонованого доступу, додаючи другий фактор (код з додатка). Налаштування: У IAM > Security credentials > Assign MFA device > Сканувати QR-код у Authy/Google Authenticator > Ввести два коди. Варіанти: Virtual MFA (додатки), Hardware MFA (токени YubiKey), U2F (USB-ключи).

### 2.3. Amazon Budgets (з другого відео)
Amazon Budgets слугує для моніторингу витрат і уникнення перевитрат. Варіанти налаштувань: Monthly budget (щомісячний ліміт), Cost budget (загальні витрати), Usage budget (за ресурсами, e.g., EC2 hours), Alert thresholds (e.g., 80% від бюджету – email-повідомлення).

### 2.4. IAM policy та дозволи (з другого відео)
IAM policy – JSON-документ, що визначає дозволи (allow/deny) для дій (e.g., "ec2:RunInstances"). Налаштування: У IAM > Policies > Create policy > JSON editor > Attach to user/group. Для користувачів: Attach policy directly або via group.

### 2.5. Варіанти додавання IAM policy при створенні користувача (з другого відео)
1. **Attach existing policies directly**: Прикріпити готові політики (e.g., AdministratorAccess).
2. **Copy permissions from existing user**: Копіювати політики з іншого користувача.
3. **Create policy**: Створити нову кастомну policy у JSON.
4. **Attach via group**: Додати до групи з політиками (не безпосередньо).

### 2.6. Писати та застосовувати політики IAM (з третього відео)
Політики пишуться в JSON: {"Version": "2012-10-17", "Statement": [{"Effect": "Allow", "Action": "s3:*", "Resource": "*"}]}. Застосовувати: IAM > Policies > Create/Attach > Select user/group/role. Для контролю: Use conditions (e.g., IP restrictions).

### 2.7. Switching IAM Roles (з третього відео)
Switching дозволяє безпечно перемикатися між ролями для доступу до ресурсів (e.g., з admin до EC2-role). Як: Console > Switch role > Ввести Account ID, Role name > Switch. Повернення: Switch back to original.

### 2.8. Permissions Boundary (з третього відео)
Permissions Boundary обмежує максимальні дозволи для ролі/користувача, запобігаючи надмірному доступу. Налаштування: IAM > Roles > Create role > Permissions boundary > Select policy (e.g., ReadOnlyAccess як ліміт).

### 2.9. CloudTrail для відстеження (з третього відео)
CloudTrail записує API-дії (who, what, when) для аудиту. Налаштування: CloudTrail > Create trail > Select regions, S3 bucket для логів > Enable. Аналіз: Query logs in Athena або view in Console.

### 2.10. Policy Simulator
Policy Simulator тестує політики: Симулює дії (e.g., s3:GetObject) для користувача/ролі, показує allow/deny. Використання: IAM > Policy Simulator > Select principal/policy > Add action/resource > Run simulation.

---

## 📋 Хід роботи

### 1. Відкриття браузера та перехід на сайт AWS
Відкрито FireFox та перейдено на [aws.amazon.com/free](https://aws.amazon.com/free). Натиснуто "Create a free AWS account".

**Скріншот 1: Головна сторінка AWS Free Tier – заблюрено для конфіденційності.**

<img width="1876" height="426" alt="Скріншот 1: Головна сторінка AWS Free Tier – заблюрено для конфіденційності." src="https://github.com/user-attachments/assets/7a842a06-3113-40eb-87f4-c6b1e02c9f28" />


Пояснення: Сторінка пропонує 12 місяців безкоштовного доступу до сервісів, таких як EC2 та S3.

### 2. Реєстрація акаунту AWS Free Tier
Кроки:
- Введено email та пароль.
- Вибрано "Personal account".
- Додано контактні дані (ім'я, адреса – заблюрено).
- Введено платіжну інформацію (картка для верифікації, $1 hold refunded).
- Вибрано Basic support plan.
- Верифіковано телефон OTP.
- Завершено sign-up.

**Скріншот 2: Форма реєстрації – email та пароль заблюрено;**

<img width="950" height="814" alt="f" src="https://github.com/user-attachments/assets/5121c333-a21d-4749-a143-f26ad0d0cab0" />

<img width="441" height="587" alt="f" src="https://github.com/user-attachments/assets/a716de01-d897-4954-8023-6d22fe30791b" />

**Скріншот 3: Billing info заблюрено;**

<img width="447" height="1206" alt="f" src="https://github.com/user-attachments/assets/d7124012-cf2a-4346-ba72-4b5351dd1916" />


**Скріншот 4: Verify phone.**

<img width="468" height="296" alt="f" src="https://github.com/user-attachments/assets/2d2f0ec8-984c-4906-b529-78c8da3fadad" />

Пояснення: Процес займає 5-10 хв. Після – доступ до Console за root credentials.

### 3. Налаштування MFA
У Console: My Security Credentials > Assign MFA device > Virtual MFA > Скановано QR у Google Authenticator > Введено коди.

**Скріншот 5: IAM Security Credentials;**
<img width="1024" height="591" alt="hd" src="https://github.com/user-attachments/assets/3dc3a1fb-45ac-4fc2-861b-2815af80a8b4" />

**Скріншот 6: QR scan in app;**
<img width="1930" height="1776" alt="hf" src="https://github.com/user-attachments/assets/e23147a5-2a90-461b-aaaa-9f1d41e48f56" />

**Скріншот 7: Success message.**
![images](https://github.com/user-attachments/assets/5e40f902-18b0-4500-94da-302ef7582752)

Пояснення: MFA активовано для root user, тепер входить з кодом з app.

### 4. Створення бюджету "Zero Spend Budget"
У Billing > Budgets > Create budget > Cost budget > Name: "Zero Spend Budget" > Set $0 threshold > Alert at 100% > Email to root.

**Скріншот 8: Create budget form;**
<img width="1024" height="278" alt="2-aws-budgets-dashboard-1024x278" src="https://github.com/user-attachments/assets/2ddfe62a-2d0f-4bb2-ab87-3717cb3bfaf2" />

**Скріншот 9: Alert configuration.**
<img width="1896" height="722" alt="Example-Picture-1-2" src="https://github.com/user-attachments/assets/4d005314-04c7-477a-bf98-da29bafeaf9a" />


Пояснення: Бюджет моніторить витрати; при >$0 – email-алерт для Free Tier compliance.

### 5. Створення IAM policy, групи та користувачів
У IAM > User groups > Create group > Name: "developers" > Attach "AdministratorAccess" policy.
Create users: "NagorniyIM" (мій), "Groupmate1", "Groupmate2" > Add to "developers" group.

**Скріншот 10: Create group;**
<img width="380" height="308" alt="new_aws_menu_1" src="https://github.com/user-attachments/assets/f438e7c1-7985-49e9-83e7-43c1b76aa3b3" />

**Скріншот 11: Attach policy;**
<img width="984" height="641" alt="cbf39fe37697b6e1dac34fdf9d61cb4e5b42593d" src="https://github.com/user-attachments/assets/f7d9c8d3-9ef6-4877-98b6-87102f682c49" />

**Скріншот 12: Create users list.**
<img width="1280" height="778" alt="add-iam-user-button" src="https://github.com/user-attachments/assets/f797c0a9-3de2-4336-8476-aae5f26ad745" />

Пояснення: Група надає повний доступ; користувачі можуть логінитися з console URL.

### 6. AWS IAM Identity Center
У IAM > Identity Center > Enable > Create group "readonly" > Attach "ReadOnlyAccess" policy.
Add user "NagorniyIM" to both groups.
View: Users > NagorniyIM > Groups: developers, readonly.

**Скріншот 13: Enable Identity Center;**
<img width="693" height="397" alt="2022-12-03-01_16_15-iam-identity-center-brave" src="https://github.com/user-attachments/assets/e0b56439-e42f-414c-9977-07303f675b1e" />

**Скріншот 14: Create readonly group;**
<img width="1536" height="579" alt="image-1536x579" src="https://github.com/user-attachments/assets/5293293b-cfaa-45da-875e-404994b86060" />

![image-1](https://github.com/user-attachments/assets/dc7d9ea9-bcb0-4790-bc45-436f04f7cae1)

<img width="1400" height="638" alt="image-1" src="https://github.com/user-attachments/assets/94fb51bd-e25c-4584-9371-b517d41d29e2" />

**Скріншот 15: User groups view.**
<img width="1273" height="575" alt="user-group-list" src="https://github.com/user-attachments/assets/ac6654e4-b7c4-4f9a-8c4b-f315c081f49a" />

Пояснення: Identity Center централізує доступ; user має ролі з обох груп (deny перекриває allow).

### 7. Встановлення AWS CLI
Завантажено з [docs.aws.amazon.com/cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) > MSI для Windows > Run installer.

**Скріншот 16: Download page;** 
<img width="1100" height="406" alt="create_folder_s3_gfg-(1)" src="https://github.com/user-attachments/assets/b4a94baa-906d-4667-acfb-7cc33dc3d1a1" />

<img width="913" height="406" alt="add_files_to_folder_s3_gfg" src="https://github.com/user-attachments/assets/9400e93b-4ca2-4448-8903-2e158b1496b0" />

**Скріншот 17: Installer progress.**
<img width="492" height="256" alt="new-soureservers-windows7" src="https://github.com/user-attachments/assets/3446014a-3fb5-4ec6-90a5-22a2012d574b" />

Пояснення: CLI v2 встановлено; перевірено `aws --version`.

### 8. Конфігурація AWS CLI
Команда: `aws configure`.
Введено Access Key ID, Secret Access Key (з IAM > Users > Security credentials), region: us-east-1, output: json.

**Скріншот 18: Terminal with aws configure;** 
<img width="979" height="512" alt="JfB7M" src="https://github.com/user-attachments/assets/feb818d7-a7bc-4700-a3f1-de98660151f1" />

**Скріншот 19: Keys заблюрено.**
<img width="892" height="447" alt="config-aggregator" src="https://github.com/user-attachments/assets/4fdadfb7-d33f-4813-b80c-28432aa91a37" />

Пояснення: CLI готовий; config файл у ~/.aws.

### 9. Перегляд віртуальних машин
Команда: `aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name]'`.

Вивід: No instances running.

**Скріншот 20: Terminal output.**
<img width="717" height="522" alt="fdsasdsxaCi" src="https://github.com/user-attachments/assets/48d18d9b-9a1f-46a2-8b40-87cd60175024" />

Пояснення: Команда показує ID та статус EC2; порожній – немає VM.

### 10. Дослідження довідкового центру AWS CLI
Переглянуто [CLI Help](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-help.html) та [Command Structure](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-commandstructure.html) + [AWS-access-key](https://www.filestash.app/aws-access-key.html).

**Файл-довідка AWS CLI (українською)**: [aws_cli_reference_uk.md](https://example.com/aws_cli_reference_uk.md) (посилання на GitHub Gist або локальний файл; вміст нижче в artifact).


---

## 📋 Контрольні питання

1. **В чому суть TOTP аутентифікації? Приклади**  
   TOTP (Time-based One-Time Password) – динамічний код, генерований на основі часу та секретного ключа для двофакторної автентифікації. Суть: Коди змінюються кожні 30 сек, запобігаючи replay-атакам. Приклади: Google Authenticator (мобільний app), Authy (з бекапом), hardware tokens (YubiKey).

2. **Формат JSON: де використовується, особливості. У AWS?**  
   JSON (JavaScript Object Notation) – легкий формат для обміну даними: ключ-значення пари (e.g., {"key": "value"}). Особливості: Читабельний, ієрархічний, підтримує масиви/об'єкти. Використовується в API, конфігах. У AWS: IAM policies, CLI output, API responses.

3. **Види Amazon API. Опис**  
   - **REST API**: HTTP-based, stateless (e.g., S3 API для GET/PUT objects).  
   - **SOAP API**: XML-based, з WSDL (legacy, e.g., старі enterprise).  
   - **GraphQL API**: Query-based для ефективного fetching (e.g., AppSync).  
   - **CLI/SDK API**: AWS CLI та SDK (Python, Java) для programmatic access.

4. **Встановлення AWS CLI під ОС**  
   - **Windows**: MSI installer з сайту.  
   - **macOS**: `brew install awscli` або pkg.  
   - **Linux**: `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" | unzip | ./aws/install`.  
   Потім `aws --version` для перевірки.

5. **Базові команди AWS CLI. Приклади**  
   - `aws s3 ls`: Список S3 buckets.  
   - `aws ec2 describe-instances`: Опис EC2 instances.  
   - `aws iam list-users`: Список IAM users.  
   - `aws configure`: Налаштування credentials.  
   - `aws help`: Загальна довідка.

---

## 📝 Висновки
Лабораторна робота дозволила успішно зареєструвати AWS Free Tier акаунт, налаштувати MFA та IAM для безпеки, створити бюджет для моніторингу та встановити AWS CLI. Ознайомлення з Console та CLI показало гнучкість AWS для хмарних проєктів. Попередня підготовка закріпила теорію, а практичні кроки (e.g., IAM groups, CLI config) підготували до реального використання. Рекомендую використовувати Free Tier для тестування EC2/S3, але моніторити витрати через Budgets.

---

## 🔗 Корисні посилання
- [AWS Free Tier](https://aws.amazon.com/free)
- [IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
- [AWS CLI Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
- Відео: [Lesson 1](https://www.youtube.com/watch?v=c-s8F0hyD2o), [Lesson 2](https://www.youtube.com/watch?v=USQU9hIj3XY), [Lesson 3](https://www.youtube.com/watch?v=oSxu9x6IYE0)

---

### 📎 Додаток: Файл-довідка AWS CLI

### Доступ до довідки
- `aws help`: Загальна довідка.
- `aws ec2 help`: Довідка по EC2.
- `aws ec2 describe-instances help`: Деталі команди.

Налаштування виведення: `cli_help_output` (terminal/browser/url).

Розділи довідки: Name, Description, Synopsis, Options, Examples, Output.

### Структура команд
Синтаксис: `aws <команда> <підкоманда> [опції]`.

Приклади:
- `aws s3 ls`: Список відер.
- `aws cloudformation create-change-set --stack-name my-stack --change-set-name my-change-set`.

Команди wait: `aws cloudformation wait change-set-create-complete ...`.

Ресурси: [Reference Guide](https://docs.aws.amazon.com/cli/latest/reference/index.html), [Troubleshooting](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-troubleshooting.html).