# Тестове завдання для вакансії PHP Developer

## Опис

Це завдання передбачає створення PHP-класів для роботи з об'єктами компаній та співробітників, включаючи валідацію полів та зв'язок між об'єктами. Завдання включає розробку базового класу `DatabaseObject`, який буде використовуватися для базових CRUD операцій, та двох класів `Company` і `Employer`, що будуть успадковувати цей базовий клас. Об'єкти повинні зберігатися в базі даних MySQL та включати функціональність для валідації полів.

## Завдання

### Загальна мета

Розробити базовий клас `DatabaseObject`, за допомогою якого можна створювати, читати, оновлювати та видаляти об'єкти в базі даних. Створити два класи, `Company` та `Employer`, які успадковуватимуть цей базовий клас. Кожен з цих класів повинен мати свій власний набір полів, що будуть валідовані при створенні або оновленні записів. Якщо валідація не проходить, об'єкт повинен містити поле `errors` з описом помилок.

### Вимоги до класів

1. **`DatabaseObject` (базовий клас)**:
    - Повинен забезпечувати основні CRUD операції (створення, читання, оновлення, видалення) для об'єктів у базі даних.
    - Повинен мати функціональність для валідації полів та збереження їх значень у базі даних.
    - Якщо валідація не проходить, методи `update` та `create` повинні повертати `false`, а в об'єкті повинно з'являтися поле `errors` з описом помилок.

2. **`Company` (імплементація класу для компаній)**:
    - Повинен успадковувати клас `DatabaseObject` і представляти таблицю в базі даних для компаній.
    - Поля для `Company`:
        - **location**: Місцезнаходження компанії. Повинно бути непорожнім рядком.
        - **industry**: Індустрія, до якої належить компанія. Повинно бути непорожнім рядком.
    - Повинна бути реалізована валідація для кожного поля.
    - При видаленні компанії всі співробітники цієї компанії також повинні бути видалені.

3. **`Employer` (імплементація класу для співробітників)**:
    - Повинен успадковувати клас `DatabaseObject` і представляти таблицю в базі даних для співробітників.
    - Поля для `Employer`:
        - **position**: Посада співробітника. Повинна бути непорожнім рядком.
        - **salary**: Зарплата співробітника. Повинна бути числовим значенням, що більше нуля.
        - **company_id**: ID компанії, до якої належить співробітник. Повинен бути валідним ID існуючого запису в таблиці `Company`.
    - Повинна бути реалізована валідація для кожного поля, включаючи перевірку на існування компанії з відповідним `company_id`. Якщо компанія не існує, об'єкт не може бути створений або оновлений, і відповідна помилка додається до поля `errors`.

## Структура проекту

- **`include\DatabaseObject.php`** - Базовий клас для роботи з об'єктами у базі даних та їх полями.
- **`include\Company.php`** - Клас для роботи з компаніями, що містить специфічні поля та валідацію.
- **`include\Employer.php`** - Клас для роботи з співробітниками, що містить специфічні поля та валідацію, а також зв'язок із компанією.
- **`include\db.php`** - Файл для підключення до бази даних.
- **`index.php`** - Файл, що демонструє використання CRUD операцій з валідацією полів.

## Інструкція з реалізації

### 1. База даних

Створіть базу даних MySQL з двома таблицями: `companies` та `employers`.

**SQL для таблиці `companies`:**
```sql
CREATE TABLE companies (
                           id INT AUTO_INCREMENT PRIMARY KEY,
                           name VARCHAR(255) NOT NULL,
                           location VARCHAR(255) NOT NULL,
                           industry VARCHAR(255) NOT NULL
);
```

**SQL для таблиці `employers`:**
```sql
CREATE TABLE employers (
                           id INT AUTO_INCREMENT PRIMARY KEY,
                           name VARCHAR(255) NOT NULL,
                           position VARCHAR(255) NOT NULL,
                           salary DECIMAL(10, 2) NOT NULL,
                           company_id INT,
                           FOREIGN KEY (company_id) REFERENCES companies(id)
);
```

### 2. Класи

Створіть три файли PHP для класів `DatabaseObject`, `Company` та `Employer` в папці `include`. В кожному з цих файлів реалізуйте відповідний клас з валідацією полів та CRUD операціями.

### 3. Підключення до бази даних

Створіть файл `db.php` для підключення до бази даних та використовуйте його в класах для виконання запитів.

### 4. Демонстрація

Створіть файл `index.php`, в якому виконайте наступні дії:

1. Створіть нову компанію та співробітника.
2. Виведіть всі компанії та співробітників.
3. Оновіть дані про компанію та співробітника.
4. Видаліть компанію та співробітника.
5. Переконайтеся, що видаляючи компанію, видаляються також всі співробітники цієї компанії.

## Результат

- При запуску головного файлу `index.php` повинно бути створено, оновлено та видалено об'єкти компаній та співробітників. 
- Всі файли проєкту розмістити в архіві
- Zip-архів `result.zip` завантажити на Google Drive, посилання надіслати на електронну адресу: `mariia.chekanina@netsolidinvest.com`