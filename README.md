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

1. В каталоге проекта выполнить команды создания папок для бэкапов (резервных/архивных копий данных), базы данных и веб-сайта (бэкенда):

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
    mkdir config
    ```

2. Создать конфигурационный файл:

    ```sh
    touch config/database.js
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
    touch index.ejs project.ejs equests.ejs
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
                <td><%= request.DataZayavki ? request.DataZayavki.toISOString().slice(0,10) : '-' %></td>
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
        <p>Система управления проектами © 2025</p>
    </footer>
    </body>
    </html>
    ```

    - Для даты используется форматирование в строку `YYYY-MM-DD`.

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

## 6 Разворачиваение компонентов
Для развертывания приложения используется среда виртуализации Docker, причем для удобства оркестрации контейнерами задействуется Docker Compose с двумя сервисами: MySQL и Node.js приложением.

### 6.1 Разворачивание БД
Необходимо развернуть БД MySQL с данными из скрипта *db/init.sql* в Docker-контейнере, чтобы данные сохранялись в примонтированном томе (`db_data:/var/lib/mysql`), определённом в *docker-compose.yml*.

Ключевые особенности:
- Все данные и структура БД будут храниться в volume `db_data`.

- При повторных перезапусках контейнера БД не будет теряться.

- Для повторной инициализации нужно просто удалить volume.

Таким образом, всё, что здесь нужно сделать — положить скрипт в папку, примонтировать его через *docker-compose.yml* в `/docker-entrypoint-initdb.d/,` и при первом запуске контейнера MySQL БД будет создана и заполнена, а все данные будут храниться в volume db_data. Если потребуется несколько файлов или дамп, то можно положить в папку *db/* несколько файлов, все они будут выполнены по алфавиту.

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

    Проверка логов контейнера:
    ```sh
    docker compose logs db
    ```

    Посмотр логов MySQL даст возможность  убедиться, что скрипт был выполнен без ошибок.

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
