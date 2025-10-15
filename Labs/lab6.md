# 📋 ЛАБОРАТОРНА РОБОТА №6

## 📌 Дисципліна: "Хмарні технології та сервіси"

## 🏷 Тема:
> Реєстрація та знайомство з хмарним середовищем Azure

## 👨‍🎓 Виконав:
- Нагорний І.М. РПЗ-24Б

---

## 🎯 Мета роботи
1. Ознайомитися з хмарним провайдером Azure.
2. Зареєструвати акаунт та дослідити інтерфейс Azure Portal.
3. Виконати практичні завдання з налаштування та використання основних сервісів Azure.

## 🛠 Матеріальне забезпечення
- 💻 Браузер з доступом до мережі Інтернет.
- 🌐 Сайт Azure: [portal.azure.com](https://portal.azure.com).

---

## 📚 Короткі теоретичні відомості
**Microsoft Azure** – це хмарна платформа, яка пропонує широкий набір сервісів для обчислень, зберігання даних, баз даних, мереж, аналітики, штучного інтелекту та DevOps.

**Основні переваги Azure:**
- **Гнучкість:** Масштабування ресурсів залежно від навантаження.
- **Pay-as-you-go:** Оплата лише за використані ресурси.
- **Інтеграція:** Сумісність із Microsoft 365 та Active Directory.
- **Глобальна інфраструктура:** Доступ до дата-центрів у понад 60 регіонах світу.

**Класифікація сервісів Azure:**
1. **Обчислення (Compute):**
   - Azure Virtual Machines (VMs): Віртуальні сервери для різноманітних задач.
   - App Services: Платформа для розгортання веб-додатків без управління інфраструктурою.
   - Azure Functions: Безсерверні обчислення для подійного програмування.
2. **Зберігання даних (Storage):**
   - Blob Storage: Об’єктне сховище для файлів.
   - Disk Storage: Блокове сховище для віртуальних машин.
3. **Бази даних (Databases):**
   - Azure SQL Database: Керована реляційна база даних.
   - Cosmos DB: NoSQL-база для глобальних додатків.
4. **Мережа (Networking):**
   - Virtual Network (VNet): Ізольовані мережі для безпеки.
   - Azure Load Balancer: Балансування мережевого навантаження.
5. **Безпека та моніторинг:**
   - Azure Active Directory (Azure AD): Управління ідентифікацією та доступом.
   - Azure Monitor: Моніторинг і аналітика ресурсів.

**Типи облікових записів:**
- **Free Account:** 200$ кредитів на 30 днів + безкоштовні ресурси на 12 місяців.
- **Student Account:** 100$ кредитів для студентів без прив’язки банківської карти.

**Azure Portal** – веб-інтерфейс для створення ресурсів, управління VM, базами даних, білінгом і безпекою.  
**Azure CLI** – інструмент командного рядка для автоматизації управління.  
*Приклади команд:*
- `az login` – авторизація в обліковому записі.
- `az group create --name LabGroup --location eastus` – створення ресурсної групи.
- `az vm list --output table` – перегляд віртуальних машин.

---

## 📚 Попередня підготовка: Відповіді на питання
Розглянуто навчальні відео:
- Microsoft Azure – що це? Огляд можливостей і приклади застосування.
- Швидкий огляд Azure Virtual Machine.
- Огляд Azure App Service.
- Azure Storage Account: Огляд та Демонстрація на C#.
- Azure Functions: Покрокове створення, написання коду у VS Code та локальний запуск.
- Azure RBAC: Що це, як працює, як налаштувати ролі та доступ.
- How to create FREE Azure Account.

### Відповіді на питання:
1. **Що таке віртуальна машина та які особливості їх реалізації у Azure Virtual Machine?**  
   Віртуальна машина (VM) – це віртуалізований сервер, що імітує фізичний комп’ютер. У Azure VM підтримує широкий вибір ОС (Windows, Linux), автоматичне масштабування, інтеграцію з Azure AD та можливість створення знімків (snapshots) для резервного копіювання.

2. **Які можливості надає Azure App Service?**  
   Azure App Service дозволяє розгортати веб-додатки (PHP, .NET, Python, Java, Node.js) без управління серверами, підтримує автоматичне масштабування, інтеграцію з CI/CD та deployment slots для тестування.

3. **Які основні кроки створення App Service через портал Azure?**  
   - Увійти в Azure Portal.
   - Вибрати "Create a resource" → "App Service".
   - Налаштувати ім’я, підписку, групу ресурсів, ОС та регіон.
   - Вибрати план ціноутворення (наприклад, Free або Shared).
   - Натиснути "Review + Create" і запустити.

4. **Які особливості реалізації "Access control (IAM)" в Azure?**  
   Azure IAM (Identity and Access Management) базується на Azure RBAC (Role-Based Access Control). Дозволяє призначати ролі користувачам або групам для доступу до ресурсів. Ролі включають Owner, Contributor, Reader тощо.

5. **Розкрийте використання Deployment slots для управління версіями.**  
   Deployment slots дозволяють створювати тестові середовища (staging) для веб-додатків. Після тестування версію можна перенести в production через "swap", мінімізуючи простої.

6. **Здійсніть огляд Storage Account та його ключових функцій.**  
   Azure Storage Account – це універсальний сервіс для зберігання даних із підтримкою Blob, File, Queue, Table Storage. Функції: масштабування, шифрування, геореплікація, підтримка доступу через API.

7. **Охарактеризуйте різні типи сховищ у Azure.**  
   - **File Storage:** Мережеві файлові шари для спільного доступу (SMB-протокол).
   - **Blob Storage:** Об’єктне сховище для великих даних (зображення, відео).
   - **Table Storage:** NoSQL-сховище для структурованих даних.
   - **Queue Storage:** Організація черг для асинхронної обробки.

8. **Опишіть як працювати з Azure Storage на прикладі використання мови C#.**  
   Використовується бібліотека Azure.Storage.Blobs. Приклад: підключення до Blob Storage, завантаження файлу через BlobClient.UploadAsync(). Потрібно налаштувати Connection String та контейнер.

9. **Що таке Serverless та особливості їх реалізації у Azure Functions?**  
   Serverless – модель, де провайдер керує інфраструктурою, а користувач пише лише код. Azure Functions підтримує тригери (HTTP, Timer, Queue), автоматичне масштабування та інтеграцію з Azure-сервісами.

10. **Поясніть різницю між автентифікацією та авторизацією. Як пов’язані Azure RBAC та Entra ID (Azure AD)?**  
   - **Автентифікація:** Перевірка особи користувача (наприклад, логін/пароль, MFA).  
   - **Авторизація:** Визначення прав доступу до ресурсів.  
   Azure AD (Entra ID) відповідає за автентифікацію, а RBAC – за авторизацію, призначаючи ролі для доступу до ресурсів.

---

## 📋 Хід роботи

### 1. Відкриття Azure Portal
- Відкрито браузер та перейдено на сайт [portal.azure.com](https://portal.azure.com).  
[Скріншот_Відкриття_Azure_Portal](https://github.com/user-attachments/assets/37fa213b-a25b-42ac-9301-f20c3fd34d1b)

### 2. Реєстрація FREE Azure Account

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

### 3. Налаштування MFA

1. **Увімкнення MFA**: Відкрийте Azure Portal ([portal.azure.com](https://portal.azure.com)), перейдіть до Azure AD → Users and Groups → All Users → Multi-Factor Authentication.  
  ![Скріншот_Налаштування_MFA](https://github.com/user-attachments/assets/d2b5652a-8e72-47f7-af98-7537cab8a969)

2. Виберіть обліковий запис Global Administrator, натисніть **Enable** у новій вкладці.  
  ![MFAAzure2](https://github.com/user-attachments/assets/14f6d93d-d003-4a79-8c0e-b6a3582f650a)

3. Підтвердіть, натиснувши **Enable Multi-Factor Auth** і **Close**. Статус MFA для облікового запису зміниться на **Enabled**.  
  ![MFAAzure3](https://github.com/user-attachments/assets/810dc1bc-4992-4dc7-a42f-eead9f6add67)

4. **Налаштування верифікації**: Під час першого входу в Azure Portal користувачу запропонують налаштувати додаткову верифікацію. Натисніть **Set it up now**.  
  ![MFAAzure4](https://github.com/user-attachments/assets/89984974-0741-4049-9f10-26ed75e237b9)

5. Виберіть метод верифікації (наприклад, Mobile app). Натисніть **Set up**.  
  ![MFAAzure5](https://github.com/user-attachments/assets/fd5943f3-1221-48e9-b1a7-f5da87271aa8)

6. Відскануйте QR-код у Microsoft Authenticator. Після налаштування натисніть **Next**.  
  ![MFAAzure6](https://github.com/user-attachments/assets/acd16a5e-67a4-4ae3-865d-462acea409ec)

7. Оберіть спосіб: **Receive notification** або **Use verification code**. У прикладі — сповіщення. Натисніть **Next**.  
  ![MFAAzure7](https://github.com/user-attachments/assets/e30a493d-bf4e-43af-b207-0a03375a1c6a)

8. Вкажіть номер телефону для резервного доступу.  
  ![MFAAzure8](https://github.com/user-attachments/assets/abccf249-1139-43a3-b689-9eeeca8ab8c5)

9. **Пароль додатка**: Azure MFA згенерує пароль додатка (не потрібен для Azure Portal/PowerShell).  
  ![MFAAzure9](https://github.com/user-attachments/assets/df19c4be-ea10-4d07-9587-623e7b7cfcc8)

10. Наступного входу Global Administrator виконає MFA за налаштованим методом.  
  ![MFAAzure10](https://github.com/user-attachments/assets/64343b3b-7f3e-4c98-9e72-81a8dbebcdfd)

11. Статус MFA для користувача зміниться на **Enforced**.  
  ![MFAAzure11](https://github.com/user-attachments/assets/d4e1fb4e-2c06-4eea-9189-fb49dbc28651)

### 4. Створення бюджету “Zero Spend Budget”
1. **Відкриття розділу бюджетів**  
   Увійдіть в Azure Portal, перейдіть до **Subscriptions**, виберіть потрібну підписку та натисніть **Budgets** у меню. Для іншого рівня (наприклад, management group) використовуйте **Scope pill** для зміни обсягу.

2. **Створення бюджету для ресурсної групи**  
   Щоб створити бюджет для ресурсної групи, у пошуковій панелі Azure Portal введіть **Resource groups**, виберіть групу, а потім знайдіть опцію **Budgets** у меню.

3. **Налаштування бюджету**  
   Натисніть **Add** для створення нового бюджету. У вікні **Create budget**:  
   - Перевірте правильність обраного **scope**.  
   - Додайте фільтри (наприклад, за ресурсними групами чи сервісами, такими як віртуальні машини).  
   - Вкажіть **назву бюджету**.  
   - Оберіть період оновлення: **Monthly**, **Quarterly** або **Annually**.  
     - Період оновлення визначає часовий проміжок аналізу. Витрати обнуляються на початку кожного періоду.  
     - Для квартального бюджету сума розподіляється рівномірно на 3 місяці, для річного — на 12 місяців.
<img width="2416" height="1355" alt="budgets-cost-management" src="https://github.com/user-attachments/assets/61d2d25b-3d92-45d0-8719-8ffb118cbab4" />

4. **Вирівнювання періоду бюджету**  
   Якщо у вас підписка типу pay-as-you-go, MSDN або Visual Studio, період рахунку може не збігатися з календарним місяцем. Виберіть:  
   - **Billing month/quarter/year** для вирівнювання з періодом рахунку.  
   - **Monthly/Quarterly/Annually** для вирівнювання з календарними місяцями.

5. **Встановлення дати закінчення**  
   Вкажіть дату, коли бюджет стане неактивним і перестане оцінювати витрати.

6. **Вибір суми бюджету**  
   На основі обраних параметрів з’явиться графік із прогнозованими витратами. Рекомендована сума бюджету базується на максимальних прогнозованих витратах. Ви можете змінити суму за потреби.
<img width="2279" height="1108" alt="create-monthly-budget" src="https://github.com/user-attachments/assets/3eb20a91-e6a2-4884-9a96-dec2611bfe91" />

7. **Налаштування сповіщень**  
   Натисніть **Next**, щоб налаштувати сповіщення для фактичних витрат та прогнозованих перевищень бюджету.

### 5. Створення групи та користувачів в Azure AD
1. **Створення групи**: У Azure Active Directory → **Groups** → **New Group**. Створіть групу, наприклад, “Developers”.  
<img width="375" height="324" alt="dataverse-team-manage-new-team" src="https://github.com/user-attachments/assets/e0fb8a5d-1db1-4bad-9a88-2ffa5cf642d9" />
<img width="375" height="390" alt="dataverse-team-manage-new-team-azuread" src="https://github.com/user-attachments/assets/cf178223-ef62-4bda-8743-b64416f36b5a" />

2. **Додавання користувачів**: Додайте учасників до групи “Developers”, наприклад: [Ваше ім’я], [Ім’я одногрупника 1], [Ім’я одногрупника 2].
<img width="1081" height="575" alt="match-azure-ad-to-dataverse" src="https://github.com/user-attachments/assets/0e43c5d3-5cff-42a0-8ad0-11d34656fc1b" />

**Типи членства в груповій робочій групі Dataverse**

| Тип членства в Dataverse | Результативна участь у групах |
|--------------------------|-------------------------------|
| Учасники та гості        | Включає типи користувачів Учасник і Гість з Microsoft Entra категорії групи Учасники. |
| Учасники                 | Включає лише тип користувача Учасник з Microsoft Entra категорії групи Учасники. |
| Відповідальні            | Включає лише тип користувача Учасник з Microsoft Entra категорії групи Власники. |
| Гості                    | Включає лише тип користувача Гість з Microsoft Entra категорії групи Учасники. |


3. **Налаштування ролі безпеки**: У Power Platform Admin Center виберіть середовище → **Settings** → **Users + permissions** → **Teams**. Створіть групову команду, вкажіть тип (наприклад, Microsoft Entra Security Group), назву та бізнес-одиницю. Призначте роль безпеки.  
<img width="375" height="302" alt="dataverse-team-manage-edit" src="https://github.com/user-attachments/assets/9a2dc83f-48d5-4eb7-9080-ee9edfd1b399" />


4. **Керування доступом**: Додайте користувачів до Microsoft Entra групи для автоматичного надання доступу до середовища. Видалення користувача з групи скасовує доступ.  
<img width="193" height="54" alt="select-team" src="https://github.com/user-attachments/assets/5eda9558-4df1-48be-a6c0-80194c490ff0" />
<img width="374" height="348" alt="dataverse-team-manage-security-roles" src="https://github.com/user-attachments/assets/7329a189-bd41-4fcb-a64c-46b11bb10df2" />

5. **Додавання типів групових робочих груп до стандартного подання підстановки**
<img width="800" height="174" alt="team-type-edit-filters" src="https://github.com/user-attachments/assets/aa8f51eb-6435-4d46-a70b-0b4d1366f166" />


### 6. Створення групи readonly
1. У Azure AD → Groups створив групу “readonly”.
2. Додав одного користувача з групи “developers”.
3. Переглянув список груп для цього користувача.  
<img width="1081" height="575" alt="match-azure-ad-to-dataverse" src="https://github.com/user-attachments/assets/a882157f-2deb-4bed-ace1-6f0d54abe3ca" />
<img width="800" height="174" alt="team-type-edit-filters" src="https://github.com/user-attachments/assets/15e924d9-7724-4f81-849e-bce02e403ce2" />

### 7. Встановлення Azure CLI
1. Завантажив Azure CLI з офіційного сайту.
2. Встановив на ПК (Windows/Linux/macOS).
3. Перевірив встановлення командою `az --version`.
![Azure-CLI-Windows-Terminal-PowerShell](https://github.com/user-attachments/assets/49814470-cf5c-4f2b-88d5-9c8897677e98)

- Azure Cloud Shell
<img width="887" height="651" alt="azure-cloud-shell" src="https://github.com/user-attachments/assets/467699df-a8be-49b8-b354-84276a884243" />


### 8. Налаштування Azure CLI
1. Виконав команду `az login`.
2. Увійшов через браузер, використовуючи обліковий запис Azure.  
<img width="988" height="514" alt="AZ Login" src="https://github.com/user-attachments/assets/9ce5f83c-3783-4ceb-a899-572ca6f571ee" />


### 9. Перегляд віртуальних машин
1. Виконав команду `az vm list --output table`.
2. Переглянув список активних віртуальних машин (жодних не виявлено).  
<img width="1148" height="443" alt="IwklZ" src="https://github.com/user-attachments/assets/b6293d38-fdf9-449a-a425-08bc87c5103f" />


### 10. Дослідження Azure CLI
1. Ознайомився з документацією:
  - [Azure CLI Documentation](https://docs.microsoft.com/en-us/cli/azure/).
  - [Choose the right Azure command-line tool](https://docs.microsoft.com/en-us/azure/cli/).
2. Створив файл-довідку українською мовою.  

## Довідка
Azure CLI — кросплатформений інструмент командного рядка для керування ресурсами Microsoft Azure. Він дозволяє автоматизувати завдання прямо з термінала.

## Основні переваги
- Працює на **Windows**, **macOS** та **Linux**.
- Доступний через [Azure Cloud Shell](https://shell.azure.com/) у браузері.
- Ідеальний для автоматизації та створення скриптів.

## Встановлення

### Windows
```bash
msiexec /i https://aka.ms/installazurecliwindows
```
Або через PowerShell:
```powershell
winget install Microsoft.AzureCLI
```

### macOS
```bash
brew update && brew install azure-cli
```

### Linux (Ubuntu/Debian)
```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

## Аутентифікація
```bash
az login
```
Відкриває браузер для входу в обліковий запис Azure.

## Основні команди
- **Перегляд підписок**:
  ```bash
  az account list
  ```

- **Створення групи ресурсів**:
  ```bash
  az group create --name Ім'яГрупи --location eastus
  ```

- **Створення віртуальної машини**:
  ```bash
  az vm create --resource-group Ім'яГрупи --name Ім'яВМ --image UbuntuLTS --admin-username azureuser --generate-ssh-keys
  ```

- **Перегляд ресурсів**:
  ```bash
  az resource list
  ```

## Оновлення Azure CLI
```bash
az upgrade
```

## Приклад автоматизації
Скрипт для створення групи ресурсів та VM:
```bash
az group create --name myGroup --location westeurope
az vm create --resource-group myGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

- Для перегляду довідки:
  ```bash
  az --help
  az <команда> --help
  ```


---

## ❓ Контрольні питання
1. **В чому суть TOTP аутентифікації? Наведіть приклади в контексті Microsoft Authenticator та Azure MFA.**  
   TOTP (Time-Based One-Time Password) – це генерація тимчасового коду на основі часу. Microsoft Authenticator генерує 6-значний код кожні 30 секунд. У Azure MFA код вводиться для підтвердження особи після логіну.

2. **Опишіть формат JSON: де він використовується, які його особливості. Чи застосовується цей формат у Azure?**  
   JSON – легкий формат обміну даними, структурований як ключ-значення. Використовується в API Azure для конфігурації ресурсів (наприклад, ARM-шаблони). Особливості: простота, підтримка вкладених структур.

3. **Які є види Azure API? Коротко опишіть їх.**  
   - **ARM API:** Управління ресурсами (створення, видалення).  
   - **Service APIs:** Доступ до сервісів (наприклад, Blob Storage).  
   - **Microsoft Graph API:** Інтеграція з Azure AD та Microsoft 365.

4. **Як можна встановити Azure CLI під різними ОС?**  
   - **Windows:** Через MSI-інсталятор або winget (`winget install -e --id Microsoft.AzureCLI`).  
   - **Linux:** Використання пакетного менеджера (наприклад, `apt install azure-cli`).  
   - **macOS:** Через Homebrew (`brew install azure-cli`).

5. **Розгляньте базові команди Azure CLI. Наведіть приклади.**  
   - `az login` – авторизація.  
   - `az group create --name MyGroup --location eastus` – створення ресурсної групи.  
   - `az vm list` – перегляд віртуальних машин.  
   - `az storage account list` – перегляд Storage Accounts.

---

## 📝 Висновки
Лабораторна робота №6 дозволила ознайомитися з Azure, його інтерфейсом і базовими сервісами. Практичні завдання допомогли освоїти створення акаунту, налаштування MFA, бюджетів, груп у Azure AD та роботу з Azure CLI. Використання англійської мови сприяло кращому розумінню документації.

---

## 🔗 Корисні посилання
- [Azure Portal](https://portal.azure.com)
- [Azure CLI Documentation](https://docs.microsoft.com/en-us/cli/azure/)
- [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Choose the right Azure command-line tool](https://learn.microsoft.com/en-us/cli/azure/choose-the-right-azure-command-line-tool?view=azure-cli-latest)
- [Azure Free Account](https://azure.microsoft.com/en-us/free/)
- [Microsoft Learn: Azure Fundamentals](https://learn.microsoft.com/en-us/azure/)
- [Microsoft Azure – що це? Огляд можливостей і приклади застосування](https://www.youtube.com/live/I4zOZPwQVEY?si=VXFV9QUFxVc35b1n)
- [Швидкий огляд Azure Virtual Machine](https://youtu.be/cDEKCTCIihM?si=VevphxDvCXRQ5mie)
- [Огляд Azure App Service](https://youtu.be/mRPc945YtkQ?si=igX-z3ZejYP9lYM8)
- [Azure Storage Account: Огляд та Демонстрація на C#](https://youtu.be/HTDHvmn9NBM?si=Jr4Vnuv0AsEFOA2I)
- [Azure Functions: Покрокове створення, написання коду у VS Code та локальний запуск](https://youtu.be/YOMF_jT9AWc?si=3eFOMB_EXBnFeVyw)
- [Azure RBAC: Що це, як працює, як налаштувати ролі та доступ](https://youtu.be/P7wdryFGTTk?si=Z6Ap8_zll6lZabpy)
- [How to create FREE Azure Account](https://youtu.be/OU1Vic_QURc?si=a5TpGEVp86DH4hO0)

---

## 🎯 Система оцінювання
- 📚 Питання попередньої підготовки: 5 балів  
- 📋 Практичні завдання з ходу роботи: 10 балів  
- ❓ Контрольні питання та висновки: 5 балів  
- 🌐 Використання англійської мови (фрагментарно): +5 балів