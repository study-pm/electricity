# Отчёт

## 1 Техническое описание системы

- Описание целей и задач практики
- Краткий обзор используемых технологий (Linux, git, GitHub, nodejs, Docker, базы данных SQL, веб-технологии);
- Обоснование выбора проекта и его значимости для формирования профессиональных компетенций.

Веб-проект на стеке:
- **ОС**: Linux
- **СКВ**: git
- **БД**: mySQL
- **Сервер**: Node.js
- **Веб-фреймворк**: Express;
- **Шаблонизатор**: EJS;
- **ORM**: Sequelize;
- **Контейнеризация**: Docker
- **Система автоматизации и развертывания**: Docker Compose.

## 2 Инсталляция программного обеспечения компьютерных систем

### 2.1 Установка и настройка операционной системы Linux. Создание пользователя с соответствующими правами

Использовать материал практических работ или любой другой доступный материал из сети.

### 2.2 Установка и настройка системы контроля версии git. Конфигурация пользователя

Установка git:
- [1.5 Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

Конфигурирование git:
- [1.6 Getting Started - First-Time Git Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

### 2.3 Установка и настройка среды разработки VSCode

Установка VSCode:
- [Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux)

Установка плагинов:

### 2.4 Установка и настройка среды контейнеризации Docker и Docker Compose на рабочей машине

Установка Docker и Docker Compose:
- [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
- [Overview of installing Docker Compose](https://docs.docker.com/compose/install/)

Конфигурирование Docker:
- [Linux post-installation steps for Docker Engine](https://docs.docker.com/engine/install/linux-postinstall/)

### 2.5 Установка кроссплатформенной среды для разработки клиентских приложений Node.js

- [Download Node.js®](https://nodejs.org/en/download)

Ваирант установки через NVM (Node Version Manager):
```sh
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"

# Download and install Node.js:
nvm install 22

# Verify the Node.js version:
node -v # Should print "v22.16.0".
nvm current # Should print "v22.16.0".

# Verify npm version:
npm -v # Should print "10.9.2".
```

Вариант установки с использованием Docker:
```sh
# Docker has specific installation instructions for each operating system.
# Please refer to the official documentation at https://docker.com/get-started/

# Pull the Node.js Docker image:
docker pull node:22-alpine

# Create a Node.js container and start a Shell session:
docker run -it --rm --entrypoint sh node:22-alpine

# Verify the Node.js version:
node -v # Should print "v22.16.0".

# Verify npm version:
npm -v # Should print "10.9.2".
```

## 3 Разработка и настройка базового системного и сервисного ПО

### 3.1 Создание репозитория на GitHub и клонирование его локально

На сайте https://github.com под своим аккаунтом создать новый проект. Задать ему имя, описание (опционально), выбрать тип проекта (публичный или приватный). Иницализировать репозиторий файлом *README.md*:

- [x] Add a README file

Клонировать проект через SSH-протокол (более безопасно):

```sh
git clone git@study-pm.github.com:study-pm/electricity.git
```

### 3.2 Создание новой ветки для разработки

1. Перейти в папку проекта:

    ```sh
    cd electricity
    ```

2. Проверить главную ветку проекта:

    ```sh
    git branch
    ```

3. Создать ветку для разработки базовой структуры и конфигурации проекта и сразу переключиться в нее:

    ```sh
    git checkout -b setup-project
    ```

4. Создать в удалённом репозитории ветку, соответствующую локальной и связать их:

    ```sh
    git push -u origin setup-project
    ```

### 3.3 Определение структуры проекта

1. В каталоге проекта выполнить команды создания папок для базы данных и веб-сайта (бэкенда):

    ```sh
    mkdir db     # папка для файлов бд
    mkdir site   # папка для веб-сайта
    ```

2. Создать файл списка игнорируемых файлов (*.gitignore*):

    ```sh
    touch .gitignore
    ```

3. Зафиксировать изменения:

    ```sh
    git add . # добавить все файлы в область отслеживания
    git commit -m 'add gitignore file' # фиксация изменений с сообщением
    ```

4. Отправить изменения на удаленный сервер:

    ```sh
    git push
    ```

5. На удаленном сервере (https://github.com) создать новый запрос на принятие изменений (Pull Request), проверить выполненные изменения и сделать слияние ветки *setup-project* с главной веткой проекта (*main*).

6. Удалить ветку *setup-project* в удаленном репозитории (кнопка *Delete Branch*).

7. Переключиться в основную ветку и забрать слитые изменения из удаленного репозитория.

    ```sh
    git checkout main # переключение в главную ветку
    git pull -p       # синхронизация с удаленным репозиторием
    ```

8. Удалить ветку *setup-project* локально:

    ```sh
    git branch -d setup-project # удаление ветки
    git branch -a               # проверка (отображение всех веток)
    ```

## 4 Разработка структуры базы данных под управлением СУБД MySQL

### 4.1 Описание сущностей

База данных *OPK12A* содержит таблицы:

- `Proekty` — проекты (id, номер, название)

- `SmejnieOborudovaniya` — смежное оборудование (связано с проектами и типами оборудования)

- `TipySmejnogoOborudovaniya` — типы оборудования

- `Sklady` — склады (с расположением)

- `Yacheiki` — ячейки на складах (связаны с оборудованием и складом)

- `Zayavki` — заявки (с номером и датой)

- `SostaviZayavok` — состав заявок (связь между ячейками и заявками)

Данные таблицы и связи позволяют реализовать функционал отображения проектов, деталей проектов с оборудованием и складами, а также список заявок с их составом.

### 4.2 Концептуальная, логическая, физическая схема БД

### 4.3 Создание схемы БД и сценария заполнения данными

1. Создать ветку для разработки структуры БД, переключиться в нее и связать с удаленной

    ```sh
    git checkout -b setup-db-scheme
    git push -u origin setup-db-scheme
    ```

2. Скрипт по созданию БД разместить в папке */db/init.sql*, добавить в область отслеживаемых файлов и зафиксировать это изменение.

    ```sh
    git add db/
    git commit -m 'add db schema and data backup'
    ```

3. Отправить изменения на удаленный сервер, сделать там слияние ветки с главной веткой проекта, переключиться в основную ветку, забрать изменения и удалить неактуальную ветку локально:

    ```sh
    git push                      # отправка изменений
    git checkout main             # переключение в главную ветку
    git pull -p                   # синхронизация с удаленным репозиторием
    git branch -d setup-db-scheme # удаление ветки
    ```

## 5 Разработка функционала веб-сервера
Для реализации backend части веб-сайта с использованием Node.js, Express и Sequelize на основе базы данных MySQL с приведённой схемой, необходимо выполнить несколько шагов. Основные моменты реализации:

- Sequelize модели отражают структуру и связи базы данных.

- Express маршруты получают данные из базы и передают их в EJS для рендеринга.

- Следует использовать асинхронный код с async/await.

- Реализовать основные страницы: проекты, детали проекта с оборудованием и складами, заявки.

- Всё это можно запускать в Docker-контейнере с настройками из Docker Compose.

Таким образом, backend будет полноценно обслуживать функционал, аналогичный исходным HTML-файлам, обеспечивая динамическую загрузку и отображение данных из MySQL с помощью Node.js, Express и Sequelize.

### 5.1 Инициализация проекта и установка зависимостей

1. Создать ветку для разработки бэкенда, переключиться в нее и связать с удаленной

    ```sh
    git checkout -b setup-backend
    git push -u origin setup-backend
    ```

2. Инициализировать проект веб-сервера и установить необходимые зависимости:

    ```sh
    cd site     # переход в папку бэкенда
    npm init -y # инициализация проекта с настройка по умолчанию
    npm install express ejs sequelize mysql2 dotenv # установка зависимостей
    ```

    - `express` — веб-фреймворк для Node.js.

    - `ejs` — шаблонизатор.

    - `sequelize` — ORM для работы с MySQL.

    - `mysql2` — драйвер MySQL.

    - `dotenv` — для работы с переменными окружения.

3. Добавить папку с библиотеками в список исключения:

    ```sh
    cd ../ # перейти в корневую папку проекта
    echo  node_modules/ >> .gitignore # добавить в исключения
    git add .gitignore # добавить файл для фиксации
    git commit -m 'ignore libs' # зафиксировать изменения
    ```

4. Зафиксировать остальные изменения:

    ```sh
    git add site # добавить все остальные файлы
    git commit -m 'install deps'
    ```

### 5.2 Настройка подключения к базе данных

1. Создать каталог для конфигурационного файла:

    ```sh
    mkdir site/config
    ```

2. Создать конфигурационный файл:

    ```sh
    touch site/config/database.js
    ```

3. Открыть проект в VSCode:

    ```sh
    code -n .
    ```

4. Заполнить файл конфигурации следующим содержимым:

    ```js
    require('dotenv').config();
    const { Sequelize } = require('sequelize');

    const sequelize = new Sequelize(process.env.DB_NAME, process.env.DB_USER, process.env.DB_PASSWORD, {
    host: process.env.DB_HOST || 'localhost',
    dialect: 'mysql',
    logging: false,
    define: {
        timestamps: false, // в базе нет полей createdAt, updatedAt
    },
    });

    module.exports = sequelize;
    ```

5. Создать файл с переменными окружения:

    ```
    cd site
    touch .env
    ```

6. В *.env* указать параметры подключения:

    ```js
    DB_HOST=db
    DB_USER=user
    DB_PASSWORD=password
    DB_NAME=OPK12A
    ```

4. Зафиксировать изменения:

    ```sh
    git add .env config/
    git commit -m 'configure db connection'
    ```

### 5.3 Определение моделей данных
Определить модели, соответствующие таблицам базы данных, с правильными связями:

- `Project` (*Proekty*)

- `Equipment` (*SmejnieOborudovaniya*)

- `EquipmentType` (*TipySmejnogoOborudovaniya*)

- `Warehouse` (*Sklady*)

- `Cell` (*Yacheiki*)

- `Request` (*Zayavki*)

- `RequestItem` (*SostaviZayavok*)

1. Создать папку *models/*

    ```sh
    mkdir models
    ```

2. В этой папке создать файлы моделей, соответствующие таблицам базы данных:

    ```sh
    cd models
    touch Project.js Equipment.js EquipmentType.js Warehouse.js Cell.js Request.js RequestItem.js
    ```

3. В VSCode заполнить файлы моделей.

    *Project.js*:
    ```js
    const { DataTypes } = require('sequelize');
    const sequelize = require('../config/database');

    const Project = sequelize.define('Proekty', {
    idProekty: {
        type: DataTypes.INTEGER,
        primaryKey: true,
        autoIncrement: true,
    },
    NomerPr: {
        type: DataTypes.STRING(45),
        unique: true,
        allowNull: false,
    },
    NazvaniePr: {
        type: DataTypes.STRING(45),
        unique: true,
        allowNull: true,
    },
    }, {
    tableName: 'Proekty',
    });

    module.exports = Project;
    ```

    *Equipment.js*:
    ```js
    const { DataTypes } = require('sequelize');
    const sequelize = require('../config/database');
    const Project = require('./Project');
    const EquipmentType = require('./EquipmentType');

    const Equipment = sequelize.define('SmejnieOborudovaniya', {
    idSmejnieOborudovaniya: { type: DataTypes.INTEGER, primaryKey: true, autoIncrement: true },
    SeriinyNomerSmejObor: { type: DataTypes.STRING(45), unique: true, allowNull: false },
    TemperaturaVozduhaSmejObor: DataTypes.INTEGER,
    TemperaturaVodySmejObor: DataTypes.INTEGER,
    TokiSmejObor: DataTypes.INTEGER,
    NapryajenieSmejObor: DataTypes.INTEGER,
    TipySmejnogoOborudovaniya_idTipySmejnogoOborudovaniya: { type: DataTypes.INTEGER, allowNull: false },
    Proekty_idProekty: { type: DataTypes.INTEGER, allowNull: false },
    }, {
    tableName: 'SmejnieOborudovaniya',
    });

    Equipment.belongsTo(Project, { foreignKey: 'Proekty_idProekty' });
    Equipment.belongsTo(EquipmentType, { foreignKey: 'TipySmejnogoOborudovaniya_idTipySmejnogoOborudovaniya' });

    module.exports = Equipment;
    ```

    *EquipmentType.js*:
    ```js
    const { DataTypes } = require('sequelize');
    const sequelize = require('../config/database');

    const EquipmentType = sequelize.define('TipySmejnogoOborudovaniya', {
    idTipySmejnogoOborudovaniya: { type: DataTypes.INTEGER, primaryKey: true, autoIncrement: true },
    NazvanieTipy: { type: DataTypes.STRING(45), unique: true, allowNull: false },
    }, {
    tableName: 'TipySmejnogoOborudovaniya',
    });

    module.exports = EquipmentType;
    ```

    *Warehouse.js*:
    ```js
    const { DataTypes } = require('sequelize');
    const sequelize = require('../config/database');

    const Warehouse = sequelize.define('Sklady', {
    idSklady: { type: DataTypes.INTEGER, primaryKey: true, autoIncrement: true },
    Raspolojenie: { type: DataTypes.STRING(45), unique: true, allowNull: false },
    }, {
    tableName: 'Sklady',
    });

    module.exports = Warehouse;
    ```

    *Cell.js*:
    ```js
    const { DataTypes } = require('sequelize');
    const sequelize = require('../config/database');
    const Warehouse = require('./Warehouse');
    const Equipment = require('./Equipment');

    const Cell = sequelize.define('Yacheiki', {
    idYacheiki: { type: DataTypes.INTEGER, primaryKey: true, autoIncrement: true },
    SeriinyNomerYacheikji: { type: DataTypes.STRING(45), unique: true, allowNull: false },
    Stoimost: DataTypes.STRING(45),
    Sklady_idSklady: { type: DataTypes.INTEGER, allowNull: false },
    SmejnieOborudovaniya_idSmejnieOborudovaniya: { type: DataTypes.INTEGER, allowNull: false },
    }, {
    tableName: 'Yacheiki',
    });

    Cell.belongsTo(Warehouse, { foreignKey: 'Sklady_idSklady' });
    Cell.belongsTo(Equipment, { foreignKey: 'SmejnieOborudovaniya_idSmejnieOborudovaniya' });

    module.exports = Cell;
    ```

    *Request.js*:
    ```js
    const { DataTypes } = require('sequelize');
    const sequelize = require('../config/database');

    const Request = sequelize.define('Zayavki', {
    idZayavki: { type: DataTypes.INTEGER, primaryKey: true, autoIncrement: true },
    NomerZayavki: { type: DataTypes.STRING(45), unique: true, allowNull: true },
    DataZayavki: { type: DataTypes.DATEONLY, allowNull: true },
    }, {
    tableName: 'Zayavki',
    });

    module.exports = Request;
    ```

    *RequestItem.js*:
    ```js
    const { DataTypes } = require('sequelize');
    const sequelize = require('../config/database');
    const Cell = require('./Cell');
    const Request = require('./Request');

    const RequestItem = sequelize.define('SostaviZayavok', {
    idSostaviZayavok: { type: DataTypes.INTEGER, primaryKey: true, autoIncrement: true },
    Yacheiki_idYacheiki: { type: DataTypes.INTEGER, allowNull: false },
    Zayavki_idZayavki: { type: DataTypes.INTEGER, allowNull: false },
    }, {
    tableName: 'SostaviZayavok',
    });

    RequestItem.belongsTo(Cell, { foreignKey: 'Yacheiki_idYacheiki' });
    RequestItem.belongsTo(Request, { foreignKey: 'Zayavki_idZayavki' });

    module.exports = RequestItem;
    ```

4. Зафиксировать изменения:

    ```sh
    git add .
    git commit -m 'define data models'
    ```

### 5.4 Определение связей между моделями

1. Создать файл *index.js* в папке *models*

    ```sh
    touch index.js
    ```

2. В этом файле собираются все модели и определяются связи между ними:

    ```js
    const sequelize = require('../config/database');

    const Project = require('./Project');
    const Equipment = require('./Equipment');
    const EquipmentType = require('./EquipmentType');
    const Warehouse = require('./Warehouse');
    const Cell = require('./Cell');
    const Request = require('./Request');
    const RequestItem = require('./RequestItem');

    // Связи (если не заданы в моделях)
    Project.hasMany(Equipment, { foreignKey: 'Proekty_idProekty' });
    Equipment.belongsTo(Project, { foreignKey: 'Proekty_idProekty' });

    Equipment.belongsTo(EquipmentType, { foreignKey: 'TipySmejnogoOborudovaniya_idTipySmejnogoOborudovaniya' });
    EquipmentType.hasMany(Equipment, { foreignKey: 'TipySmejnogoOborudovaniya_idTipySmejnogoOborudovaniya' });

    Warehouse.hasMany(Cell, { foreignKey: 'Sklady_idSklady' });
    Cell.belongsTo(Warehouse, { foreignKey: 'Sklady_idSklady' });

    Equipment.hasMany(Cell, { foreignKey: 'SmejnieOborudovaniya_idSmejnieOborudovaniya' });
    Cell.belongsTo(Equipment, { foreignKey: 'SmejnieOborudovaniya_idSmejnieOborudovaniya' });

    Request.hasMany(RequestItem, { foreignKey: 'Zayavki_idZayavki' });
    RequestItem.belongsTo(Request, { foreignKey: 'Zayavki_idZayavki' });

    Cell.hasMany(RequestItem, { foreignKey: 'Yacheiki_idYacheiki' });
    RequestItem.belongsTo(Cell, { foreignKey: 'Yacheiki_idYacheiki' });

    module.exports = {
    sequelize,
    Project,
    Equipment,
    EquipmentType,
    Warehouse,
    Cell,
    Request,
    RequestItem,
    };
    ```

3. Зафиксировать изменения:

    ```sh
    git add .
    git commit -m 'define object mapping'
    ```

### 5.5 Создание Express-приложения
Необходимо создать приложение, запускающее сервер и выполняющее базовую маршрутизацию. Маршруты Express:

- */projects* — список проектов (для главной страницы)

- */projects/:id* — детали проекта с оборудованием и складами

- */requests* — список заявок с количеством позиций и общей стоимостью

В каждом маршруте получаются данные из базы через Sequelize и рендерятся EJS-шаблоны.

1. Создать файл веб-приложения в папке *site*:

    ```sh
    cd ../
    touch app.js
    ```

2. Открыть файл в VSCode и заполнить следующим содержимым:

    ```js
    require('dotenv').config();
    const express = require('express');
    const path = require('path');
    const { sequelize, Project, Equipment, EquipmentType, Warehouse, Cell, Request, RequestItem } = require('./models');

    const app = express();

    app.set('view engine', 'ejs');
    app.set('views', path.join(__dirname, 'views'));

    app.use(express.static(path.join(__dirname, 'public')));

    // Главная страница: список проектов
    app.get('/', async (req, res) => {
    const projects = await Project.findAll();
    res.render('index', { projects }); // projects — массив объектов проектов
    });

    // Детали проекта
    app.get('/projects/:id', async (req, res) => {
    const projectId = req.params.id;

    // Получаем проект
    const project = await Project.findByPk(projectId);
    if (!project) return res.status(404).send('Проект не найден');

    // Получаем оборудование проекта с типом
    const equipment = await Equipment.findAll({
        where: { Proekty_idProekty: projectId },
        include: [EquipmentType],
    });

    // Получаем склады и ячейки с оборудованием для проекта
    const warehouses = await Warehouse.findAll({
        include: {
        model: Cell,
        include: {
            model: Equipment,
            where: { Proekty_idProekty: projectId },
            required: false,
        },
        },
    });

    res.render('project', { project, equipment, warehouses });
    });

    // Список заявок
    app.get('/requests', async (req, res) => {
    // Получаем заявки с количеством позиций и общей стоимостью
    const requests = await Request.findAll({
        include: {
        model: RequestItem,
        include: {
            model: Cell,
        },
        },
    });

    // Подсчёт количества позиций и общей стоимости для каждой заявки
    const requestsData = requests.map(req => {
        const positionsCount = req.SostaviZayavoks.length;
        const totalCost = req.SostaviZayavoks.reduce((sum, item) => {
        const cost = parseFloat(item.Yacheiki.Stoimost) || 0;
        return sum + cost;
        }, 0);
        return {
        idZayavki: req.idZayavki,
        NomerZayavki: req.NomerZayavki,
        DataZayavki: req.DataZayavki,
        positionsCount,
        totalCost,
        };
    });

    res.render('requests', { requests: requestsData });
    });

    // Запуск сервера и проверка подключения к БД
    const PORT = process.env.PORT || 3000;
    sequelize.authenticate()
    .then(() => {
        console.log('Подключение к базе данных успешно');
        app.listen(PORT, () => console.log(`Сервер запущен на порту ${PORT}`));
    })
    .catch(err => {
        console.error('Ошибка подключения к базе данных:', err);
    });
    ```

3. Зафиксировать изменения:

    ```sh
    git add .
    git commit -m 'add backend application'
    ```

### 5.6 Отображение (рендеринг) и передача данных в EJS
В маршрутах Express (в *app.js*) после получения данных из базы через Sequelize вызывается метод `res.render()`, который рендерит EJS-шаблон и передаёт в него объект с данными.

- В *views/index.ejs* выводится список проектов с ссылками на детали.

- В *views/project.ejs* выводится основная информацию о проекте, таблица оборудования и информация о складах и ячейках.

- В *views/requests.ejs* выводится таблица заявок с их данными.

Пример для главной страницы со списком проектов:
```js
app.get('/', async (req, res) => {
  const projects = await Project.findAll();
  res.render('index', { projects }); // projects — массив объектов проектов
});
```

В шаблоне *views/index.ejs* можно обращаться к переменной `projects`.

Ключевые особенности:
- Данные из базы передаются в шаблон как объекты или массивы.

- В EJS происходит динамическое построение HTML с учётом содержимого.

- Это позволяет создавать страницы, аналогичные исходным HTML-файлам, но с динамическим наполнением из MySQL через Sequelize и Express.

Основные приёмы работы с EJS
- Вставка переменных: `<%= variable %>` — вывод с экранированием.

- Логика: `<% if (...) { %> ... <% } %>`, циклы `<% array.forEach(...) { %> ... <% }) %>`.

- Проверка наличия данных для вывода сообщений об отсутствии.

- Вложенные циклы для сложных структур (например, склады → ячейки → оборудование).


Таким образом реализуется динамическое отображение данных, полученных из базы, с помощью шаблонизатора EJS, что обеспечивает полноценный функционал сайта по управлению проектами, оборудованием и заявками. Алгоритм действий:

1. Создать папку для хранения шаблонов:

    ```sh
    mkdir views
    ```

2. Создать файлы шаблонов:

    ```sh
    cd views
    touch index.ejs project.ejs requests.ejs
    ```

3. Открыть и заполнить файлы шаблонов в VSCode.

    *views/index.ejs — список проектов*:
    ```js
    <!DOCTYPE html>
    <html lang="ru">
    <head>
    <meta charset="UTF-8" />
    <title>Проекты</title>
    <link rel="stylesheet" href="/css/style.css" />
    </head>
    <body>
    <header>
        <h1>Проекты</h1>
        <nav>
        <a href="/">Проекты</a>
        <a href="/requests">Заявки</a>
        </nav>
    </header>

    <main>
        <div id="projects-list" class="grid-container">
        <% if (projects.length === 0) { %>
            <p>Проекты не найдены.</p>
        <% } else { %>
            <% projects.forEach(project => { %>
            <div class="project-item">
                <h2><a href="/projects/<%= project.idProekty %>"><%= project.NazvaniePr %></a></h2>
                <p>Номер проекта: <%= project.NomerPr %></p>
            </div>
            <% }) %>
        <% } %>
        </div>
    </main>

    <footer>
        <p>Система управления проектами © 2025</p>
    </footer>
    </body>
    </html>
    ```

    - Цикл `<% projects.forEach(...) %>` выводит каждый проект.

    - Ссылка ведёт на страницу деталей проекта `/projects/:id`.

    *views/project.ejs — детали проекта*:
    ```js
    <!DOCTYPE html>
    <html lang="ru">
    <head>
    <meta charset="UTF-8" />
    <title>Детали проекта: <%= project.NazvaniePr %></title>
    <link rel="stylesheet" href="/css/style.css" />
    </head>
    <body>
    <header>
        <h1 id="project-title"><%= project.NazvaniePr %></h1>
        <nav>
        <a href="/">Назад к проектам</a>
        <a href="/requests">Заявки</a>
        </nav>
    </header>

    <main>
        <section id="project-info">
        <h2>Основная информация</h2>
        <div class="info-grid">
            <div>Номер проекта:</div>
            <div><%= project.NomerPr %></div>
            <div>Название:</div>
            <div><%= project.NazvaniePr %></div>
        </div>
        </section>

        <section id="equipment-section">
        <h2>Оборудование</h2>
        <table id="equipment-table">
            <thead>
            <tr>
                <th>Тип</th>
                <th>Серийный номер</th>
                <th>Темп. воздуха</th>
                <th>Темп. воды</th>
                <th>Ток</th>
                <th>Напряжение</th>
            </tr>
            </thead>
            <tbody>
            <% if (equipment.length === 0) { %>
                <tr><td colspan="6">Оборудование не найдено</td></tr>
            <% } else { %>
                <% equipment.forEach(eq => { %>
                <tr>
                    <td><%= eq.TipySmejnogoOborudovaniya.NazvanieTipy %></td>
                    <td><%= eq.SeriinyNomerSmejObor %></td>
                    <td><%= eq.TemperaturaVozduhaSmejObor || '-' %></td>
                    <td><%= eq.TemperaturaVodySmejObor || '-' %></td>
                    <td><%= eq.TokiSmejObor || '-' %></td>
                    <td><%= eq.NapryajenieSmejObor || '-' %></td>
                </tr>
                <% }) %>
            <% } %>
            </tbody>
        </table>
        </section>

        <section id="warehouse-section">
        <h2>Склады</h2>
        <% if (warehouses.length === 0) { %>
            <p>Склады не найдены.</p>
        <% } else { %>
            <% warehouses.forEach(warehouse => { %>
            <div class="warehouse">
                <h3><%= warehouse.Raspolojenie %></h3>
                <% if (warehouse.Yacheikis.length === 0) { %>
                <p>Ячейки отсутствуют</p>
                <% } else { %>
                <ul>
                    <% warehouse.Yacheikis.forEach(cell => { %>
                    <% if(cell.SmejnieOborudovaniya && cell.SmejnieOborudovaniya.Proekty_idProekty === project.idProekty) { %>
                        <li>
                        Ячейка: <%= cell.SeriinyNomerYacheikji %>, Стоимость: <%= cell.Stoimost || 'не указана' %>, Оборудование: <%= cell.SmejnieOborudovaniya.SeriinyNomerSmejObor %>
                        </li>
                    <% } %>
                    <% }) %>
                </ul>
                <% } %>
            </div>
            <% }) %>
        <% } %>
        </section>
    </main>

    <footer>
        <p>Система управления проектами © 2025</p>
    </footer>
    </body>
    </html>
    ```

    - Используются вложенные циклы для вывода складов и ячеек.

    - Проверяется наличие данных, чтобы избежать пустых таблиц.

    *views/requests.ejs — список заявок*:
    ```js
    <!DOCTYPE html>
    <html lang="ru">
    <head>
    <meta charset="UTF-8" />
    <title>Заявки</title>
    <link rel="stylesheet" href="/css/style.css" />
    </head>
    <body>
    <header>
        <h1>Заявки</h1>
        <nav>
        <a href="/">Проекты</a>
        <a href="/requests">Заявки</a>
        </nav>
    </header>

    <main>
        <table id="requests-table">
        <thead>
            <tr>
            <th>Номер заявки</th>
            <th>Дата</th>
            <th>Количество позиций</th>
            <th>Общая стоимость</th>
            <th>Действия</th>
            </tr>
        </thead>
        <tbody>
            <% if (requests.length === 0) { %>
            <tr><td colspan="5">Заявки не найдены</td></tr>
            <% } else { %>
            <% requests.forEach(request => { %>
                <tr>
                <td><%= request.NomerZayavki || '-' %></td>
                <td><%= request.DataZayavki || '-' %></td>
                <td><%= request.positionsCount %></td>
                <td><%= request.totalCost.toFixed(2) %></td>
                <td>
                    <a href="/requests/<%= request.idZayavki %>">Просмотр</a>
                </td>
                </tr>
            <% }) %>
            <% } %>
        </tbody>
        </table>
    </main>

    <footer>
        <p>Система управления проектами © 2024</p>
    </footer>
    </body>
    </html>

    ```

    - Выводятся подсчитанные из контроллера количество позиций и общая стоимость.

4. Зафиксировать изменения:

    ```sh
    git add .
    git commit -m 'add view templates'
    ```

5. Отправить изменения на удаленный сервер, сделать там слияние ветки с главной веткой проекта, переключиться в основную ветку, забрать изменения и удалить неактуальную ветку локально:

    ```sh
    git push                      # отправка изменений
    git checkout main             # переключение в главную ветку
    git pull -p                   # синхронизация с удаленным репозиторием
    git branch -d setup-backend   # удаление ветки
    ```

## 6 Разворачивание компонентов
Для развертывания приложения используется среда виртуализации Docker, причем для удобства оркестрации контейнерами задействуется Docker Compose с двумя сервисами: MySQL и Node.js приложением.

### 6.1 Разворачивание БД
Необходимо развернуть БД MySQL с данными из скрипта *db/init.sql* в Docker-контейнере, чтобы данные сохранялись в примонтированном томе (`/db/data:/var/lib/mysql`), определённом в *docker-compose.yml*.

Ключевые особенности:
- Все данные и структура БД будут храниться в volume `data`.

- При повторных перезапусках контейнера БД не будет теряться.

- Для повторной инициализации нужно просто удалить volume.

Таким образом, всё, что здесь нужно сделать — положить скрипт в папку, примонтировать его через *docker-compose.yml* в `/docker-entrypoint-initdb.d/,` и при первом запуске контейнера MySQL БД будет создана и заполнена, а все данные будут храниться в volume db/data. Если потребуется несколько файлов или дамп, то можно положить в папку *db/* несколько файлов, все они будут выполнены по алфавиту.

1. Создать ветку для развертывания приложения, переключиться в нее и связать с удаленной

    ```sh
    git checkout -b app-deploy
    git push -u origin app-deploy
    ```

2. Создать в корне проекта файл *docker-compose.yml*:

    ```sh
    touch docker-compose.yml
    ```

3. Открыть файл в VSCode и заполнить его следующим содержимым:

    ```yaml
    services:
        db:
            image: mysql:8
            environment:
                MYSQL_ROOT_PASSWORD: rootpassword
                MYSQL_DATABASE: OPK12A
                MYSQL_USER: user
                MYSQL_PASSWORD: password
            ports:
                - "3306:3306"
            volumes:
                - ./db/data:/var/lib/mysql
                - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql:ro

    volumes:
        db_data:
    ```

    Пояснения:

    - `./db_data:/var/lib/mysql` — все данные БД будут храниться в локально в папке проекта (и, соответственно, будут доступны в пристыкованном к ней томе), даже после перезапуска контейнера.

    - `./db/init.sql:/docker-entrypoint-initdb.d/init.sql:ro` — при первом запуске контейнера MySQL выполнит этот скрипт, создаст структуру и наполнит БД начальными данными.

    Как работает инициализация:
    - *init.sql* будет выполнен только при первом запуске, когда volume `db_data` ещё пустой.

    - Если volume уже существует (БД уже была создана), скрипт повторно не выполнится.

    - Если нужно пересоздать БД — удалить `volume` командой:

        ```sh
        docker compose down -v
        ```

    Это удалит volume и при следующем запуске БД инициализируется заново.

    Флаг `-v` в команде `docker compose down -v` означает, что вместе с остановкой и удалением контейнеров будут удалены также все тома (volumes), которые были созданы для этих контейнеров. Это позволяет полностью очистить все данные, связанные с сервисами, включая данные, сохранённые в томах. Иными словами, команда остановит и удалит контейнеры, сети и тома, определённые в *docker-compose.yml* файле. Без флага `-v` тома сохраняются, чтобы данные не потерялись при повторном запуске контейнеров. Следует использовать `-v`, если необходимо полностью удалить все связанные данные.

4. Запуск контейнера с БД:

    ```sh
    docker compose up -d # Вариант 1
    docker-compose up -d # Вариант 2
    ```

    Разница между `docker-compose` и `docker compose` заключается в их происхождении, реализации и интеграции с Docker CLI:

    - `docker-compose` — это оригинальное автономное приложение, написанное на Python, для оркестрации многоконтейнерных приложений Docker. Оно использовалось долгое время как отдельный инструмент и устанавливалось отдельно от Docker. Команды выглядели как `docker-compose up`, `docker-compose down` и т.д.

    - `docker compose` (с пробелом) — это более новая версия Docker Compose, переписанная на Go и интегрированная непосредственно в основной Docker CLI. Она является частью ветки Compose v2 и поставляется вместе с Docker (например, в Docker Desktop). Команды теперь вызываются через основной Docker CLI, например, `docker compose up`. Это обеспечивает единообразие флагов и опций с другими командами Docker, улучшенную поддержку и обновления

    Таким образом, `docker compose` — это современный, более интегрированный и поддерживаемый инструмент, который заменяет `docker-compose`. Рекомендуется переходить на использование `docker compose` для новых проектов и обновлять скрипты, заменяя дефис на пробел в командах.

    В результате выполнения команды Docker скачает все необходимые образы и запустит сервис. Консольный вывод:
    ```
    [+] Running 11/11
    ✔ db Pulled                                                                                                                                                                                                                            13.9s 
    ✔ c2eb5d06bfea Pull complete                                                                                                                                                                                                          2.8s 
    ✔ 253ce0d09858 Pull complete                                                                                                                                                                                                          2.8s 
    ✔ 80d03d2c4741 Pull complete                                                                                                                                                                                                          2.8s 
    ✔ e4440634f2d6 Pull complete                                                                                                                                                                                                          3.0s 
    ✔ 398e77186e87 Pull complete                                                                                                                                                                                                          3.0s 
    ✔ ff3f8be14317 Pull complete                                                                                                                                                                                                          3.0s 
    ✔ 7c52b30fb2be Pull complete                                                                                                                                                                                                          4.6s 
    ✔ eb0fdd6a2898 Pull complete                                                                                                                                                                                                          4.6s 
    ✔ 61a34481c5ea Pull complete                                                                                                                                                                                                         11.9s 
    ✔ 41f706ab26e6 Pull complete                                                                                                                                                                                                         12.0s 
    [+] Running 3/3
    ✔ Network electricity_default   Created                                                                                                                                                                                                 0.2s 
    ✔ Volume "electricity_db_data"  Created                                                                                                                                                                                                 0.0s 
    ✔ Container electricity-db-1    Started    
    ```

5. Проверка правильности развертывания БД.

    Выполняется проверка того, что БД развернулась и данные на месте (получить содержимое базы данных).

    Через `docker compose` подключиться к MySQL и выполнить запросы:
    ```sh
    docker compose exec db mysql -uuser -ppassword -e "SHOW DATABASES;"
    ```

    Если контейнеры еще не успели полноценно развернуться, то можно получить следующую ошибку в консоли:
    ```
    ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
    ```

    или такую:
    ```
    ERROR 1045 (28000): Access denied for user 'user'@'localhost' (using password: YES)
    ```

    В этом случае нужно немного подождать и повторить команду. В случае успеха должен быть следующий консольный вывод:
    ```
    mysql: [Warning] Using a password on the command line interface can be insecure.
    +--------------------+
    | Database           |
    +--------------------+
    | OPK12A             |
    | information_schema |
    | performance_schema |
    +--------------------+
    ```

    Поскольку база инициализирована, то можно увидить среди баз данных *OPK12A*. 

    Показать таблицы базы:
    ```sh
    docker compose exec db mysql -uuser -ppassword -e "USE OPK12A; SHOW TABLES;"
    ```

    Консольный вывод:
    ```
    mysql: [Warning] Using a password on the command line interface can be insecure.
    +---------------------------+
    | Tables_in_OPK12A          |
    +---------------------------+
    | Proekty                   |
    | Sklady                    |
    | SmejnieOborudovaniya      |
    | SostaviZayavok            |
    | TipySmejnogoOborudovaniya |
    | Yacheiki                  |
    | Zayavki                   |
    +---------------------------+
    ```

    Показать данные (например, из таблицы проектов):
    ```sh
    docker compose exec db mysql -uuser -ppassword -e "USE OPK12A; SELECT * FROM Proekty;"
    ```

    Консольный вывод:
    ```
    +-----------+---------+----------------+
    | idProekty | NomerPr | NazvaniePr     |
    +-----------+---------+----------------+
    |         1 | 52300   | Арктика |
    |         2 | 53201   | Ермак     |
    |         3 | 5543    | Ясень     |
    |         4 | 5698-б | Бальзам |
    |         5 | 2045    | Клубень |
    |         6 | 21445   | Крюйс     |
    +-----------+---------+----------------+
    ```

    Проверка логов контейнера:
    ```sh
    docker compose logs db
    ```

    Посмотр логов MySQL даст возможность  убедиться, что скрипт был выполнен без ошибок.

6. Файлы базы данных необходимо игнорировать:

    ```sh
    echo /db/data/ >> .gitignore
    git add .gitignore && git commit -m 'ignore db files'
    ```

7. Зафиксировать изменения:

    ```sh
    git add . && git commit -m 'setup db service'
    ```

### 6.2 Разворачивание веб-приложения
Необходимо упаковать Node.js-приложение в единый контейнер, который можно запустить на любом сервере, где есть Docker. Для этого необходимо создать Dockerfile, который описывает всё, что нужно для работы приложения (код, зависимости, настройки). Docker сам скачает Node.js, установит зависимости и подготовит среду. *Dockerfile* позволяет запускать приложение как сервис в `docker compose.yml` — вместе с базой данных и другими сервисами. Контейнер работает изолированно от основной системы. Всё, что делает приложение, не влияет на хостовую ОС и наоборот.

1. Создать в корне проекта файл *Dockerfile*:

    ```sh
    touch Dockerfile
    ```

2. Открыть файл в VSCode и заполнить его следующим содержимым:

    ```dockerfile
    FROM node:18-alpine
    # Базовый образ: минимальная версия Linux с Node.js 18.
    # Это экономит место и ускоряет загрузку.

    WORKDIR /app
    # Рабочая директория внутри контейнера. Все дальнейшие команды будут выполняться здесь.

    COPY site/package*.json ./
    # Копируются файлы зависимостей (package.json и package-lock.json).

    RUN npm install
    # Устанавливаются все npm-зависимости.

    COPY site/. .
    # Копируется весь исходный код приложения внутрь контейнера.

    EXPOSE 3000
    # Оповещает Docker, что приложение слушает порт 3000 (стандарт для Express).

    CMD ["node", "app.js"]
    # Запускает приложение командой node app.js при старте контейнера.
    ```

    В данном файле учтено, что основной код лежит в подкаталоге, а не в корне (*Dockerfile* копирует файлы из папки *site*).

3. Открыть файл *docker-compose.yml* в VSCode и добавить сервис веб-приложения на бэкенде:

    ```yml
    services:
    db:
        image: mysql:8
        environment:
            MYSQL_ROOT_PASSWORD: rootpassword
            MYSQL_DATABASE: OPK12A
            MYSQL_USER: user
            MYSQL_PASSWORD: password
        ports:
            - "3306:3306"
        volumes:
            - ./db/data:/var/lib/mysql
            - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql:ro

    app:
        build:
            context: ./site
        ports:
            - "3000:3000"
        environment:
            DB_HOST: db
            DB_USER: user
            DB_PASSWORD: password
            DB_NAME: OPK12A
        depends_on:
            - db
        volumes:
            - ./site:/app

    volumes:
        db_data:

    ```

    Здесь учитывается контекст сборки: теперь это папка *site*, а не корень проекта. Особенности:

    - Если используется volume `./site:/app`, то при запуске контейнера содержимое папки *site* будет доступно внутри контейнера по пути */app*, и запуск `node app.js` будет работать.

    - Если используются оба метода (и копирование в *Dockerfile*, и volume), то volume "перекроет" то, что было скопировано на этапе сборки.


4. Запустить проект:

    ```sh
    docker compose up -d
    ```

5. Запустить веб-обозреватель и проследователь по адресу http://localhost:3000/. Должна открыться главная страница проекта.

6. Зафиксировать изменения:

    ```sh
    git add . && git commit -m 'setup web app service'
    ```

7. Отправить изменения на удаленный сервер, сделать там слияние ветки с главной веткой проекта, переключиться в основную ветку, забрать изменения и удалить неактуальную ветку локально:

    ```sh
    git push                      # отправка изменений
    git checkout main             # переключение в главную ветку
    git pull -p                   # синхронизация с удаленным репозиторием
    git branch -d app-deploy      # удаление ветки
    ```

## Тестирование и отладка

### Ошибка подключения
При попытке запуске проекта можно столкнуться с различными ошибками. Например, по какой-либо причине тот или иной контейнер может быть аварийно остановлен. Наличие работающих контейнерв можно проверить командой `docker ps`:

```sh
docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                                  NAMES
a7d10b393d7e   mysql:8   "docker-entrypoint.s…"   4 seconds ago   Up 4 seconds   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   electricity-db-1
```

В данном случае отсутствует контейнер веб-приложения. Если проверить все контейнеры, то можно убедиться в том, что он преждевременно завершил свою работу:
```sh
docker ps -a
CONTAINER ID   IMAGE             COMMAND                  CREATED              STATUS                          PORTS                                                  NAMES
d737f255446f   electricity-app   "docker-entrypoint.s…"   About a minute ago   Exited (0) About a minute ago                                                          electricity-app-1
a7d10b393d7e   mysql:8           "docker-entrypoint.s…"   About a minute ago   Up About a minute               0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   electricity-db-1
```

Можно проверить логи контейнера:
```
docker compose logs app
app-1  | Ошибка подключения к базе данных: ConnectionRefusedError [SequelizeConnectionRefusedError]: connect ECONNREFUSED 172.18.0.2:3306
app-1  |     at ConnectionManager.connect (/app/node_modules/sequelize/lib/dialects/mysql/connection-manager.js:92:17)
app-1  |     at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
app-1  |     at async ConnectionManager._connect (/app/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:222:24)
app-1  |     at async /app/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:174:32
app-1  |     at async ConnectionManager.getConnection (/app/node_modules/sequelize/lib/dialects/abstract/connection-manager.js:197:7)
app-1  |     at async /app/node_modules/sequelize/lib/sequelize.js:305:26
app-1  |     at async Sequelize.authenticate (/app/node_modules/sequelize/lib/sequelize.js:457:5) {
app-1  |   parent: Error: connect ECONNREFUSED 172.18.0.2:3306
app-1  |       at TCPConnectWrap.afterConnect [as oncomplete] (node:net:1555:16) {
app-1  |     errno: -111,
app-1  |     code: 'ECONNREFUSED',
app-1  |     syscall: 'connect',
app-1  |     address: '172.18.0.2',
app-1  |     port: 3306,
app-1  |     fatal: true
app-1  |   },
app-1  |   original: Error: connect ECONNREFUSED 172.18.0.2:3306
app-1  |       at TCPConnectWrap.afterConnect [as oncomplete] (node:net:1555:16) {
app-1  |     errno: -111,
app-1  |     code: 'ECONNREFUSED',
app-1  |     syscall: 'connect',
app-1  |     address: '172.18.0.2',
app-1  |     port: 3306,
app-1  |     fatal: true
app-1  |   }
app-1  | }
```

Обращает на себя внимание следующая проблема:
```
Ошибка подключения к базе данных: ConnectionRefusedError [SequelizeConnectionRefusedError]: connect ECONNREFUSED 172.18.0.2:3306
```

Дале излагается алгоритм проверки и отладки с изложением причин и предлагаемых решений.

1. MySQL ещё не успел запуститься. Это самая частая причина. Контейнер с приложением стартует раньше, чем база данных готова принимать подключения. Решения:

    - Убедиться, что в коде Node.js есть повторные попытки подключения (retry) или задержка перед первым запросом.

    - Можно добавить небольшую задержку старта приложения (например, через npm-пакет wait-port или wait-for-it.sh).

    - В `docker compose` `depends_on` НЕ гарантирует, что база уже готова, он только запускает контейнеры в нужном порядке.

2. Проверить логи MySQL. Посмотреть, нет ли ошибок инициализации базы, например:

    ```sh
    docker compose logs db
    ```

    Если есть ошибки (например, из-за скрипта инициализации), MySQL может не стартовать. Необходимо исправить указанные ошибки.

3. Проверить порт и имя хоста. В `docker compose` для Node.js приложения должно быть:

    ```js
    environment:
    DB_HOST: db
    DB_USER: user
    DB_PASSWORD: password
    DB_NAME: OPK12A
    ```

    где db — имя сервиса MySQL в `docker compose`.

    В Sequelize-конфигураторе необходимо использовать эти переменные.

4. Проверить что база MySQL реально слушает порт 3306:

    ```sh
    docker compose exec db netstat -ln | grep 3306
    ```

5. Проверить, что база инициализирована корректно

    Если только что создан volume с данными, и инициализационный скрипт был некорректен, база может не стартовать.

6. Перезапустить сервисы:

    ```sh
    docker compose down
    docker compose up -d
    ```

7. Если всё хорошо, но ошибка повторяется, то следует добавить retry-подключение в код Node.js.

    Retry должен быть только там, где происходит инициализация подключения к БД, то есть при вызове `sequelize.authenticate()` или при создании самого экземпляра Sequelize. Легче всего добавить функцию переподключения в конец главного файл веб-приложения *app.js* и изменить метод запуска сервера:
    ```js
    ...
    // Функция для повторных попыток подключения к БД
    async function connectWithRetry(retries = 10, delay = 3000) {
    for (let i = 0; i < retries; i++) {
        try {
        await sequelize.authenticate();
        console.log('Подключение к базе данных успешно');
        return;
        } catch (err) {
        console.error(`Ошибка подключения к базе данных (попытка ${i + 1}):`, err.message);
        if (i < retries - 1) {
            await new Promise(res => setTimeout(res, delay));
        } else {
            throw err;
        }
        }
    }
    }

    // Запуск сервера только после успешного подключения к БД
    const PORT = process.env.PORT || 3000;
    connectWithRetry()
    .then(() => {
        app.listen(PORT, () => console.log(`Сервер запущен на порту ${PORT}`));
    })
    .catch(err => {
        console.error('Не удалось подключиться к базе данных. Завершение работы.');
        process.exit(1);
    });
    ```

8. Перезапустить сервисы:

    ```sh
    docker compose down
    docker compose up -d
    ```
