# ОПИСАНИЕ РЕШЕНИЯ
## Модульные тесты
Модульные тесты находятся в файле **test.js**  

`npm run test:u` - запустить модульные тесты

Блоки:
- Блок получения данных из коммандной строки
  - получение истории коммитов
  - получение списка файлов для выбранного коммита
  - получение содержимого выбранного файла

- Блок навигации
  - формирование "хлебных крошек"
  - формирование пути (к файловой структуре и содержимому файла)

Для того, чтобы можно было проще добавить точки расширения я создал `class Git` (для получения списка коммитов, файлов и содержимого файла), в котором присваиваю методу класса `this.executeGit = executeGit`. В тестах я подменяю метод this.executeGit на свой.  
Функция `parseHistoryItem` и `parseFileTreeItem` не являются публичными интерфейсами и используются только внутри класса, поэтому их не тестирую отдельно.  

Также не писал тесты для функций `buildFolderUrl(parentHash, path = '') { ... }` и `buildFileUrl(parentHash, path) { ... }` так как они просто возвращают шаблонную строку, и даже если их и тестировать — при параметре `parentHash = undefined` они падают.  

Установил istanbul для просмотра информации о покрытии кода тестами.  
После просмотра отчета о покрытии кода тестами также написал тесты для функций, которые всего-навсего возвращают шаблонную строку из хэша и пути. Логика этих функций совсем простая, но покрыл их тестами для большего процента в отчете istanbul.  

## Интеграционные тесты
Интеграционные тесты находятся в **hermione/test.js**  

### Установка selenium
`npm install selenium-standalone --global`  
`selenium-standalone install`  
**hermione** и **html-reporter** установятся из package.json (`npm install`)  

### Запуск интеграционных тестов:
`npm run start` - стартовать локальный сервер  
`npm run selenium` - стартовать selenium (запускать в отдельном терминале)  
`npm run test:i` - выполнить интеграционные тесты (запускать в отдельном терминале)  

На главной странице обернул блоки `.commit` в блок `.history` для более удобного поиска элемента на странице.  
С этой же целью на странице с файловой системой для тега ul добавил класс `files-tree`.  

**hermione-html-report на windows** открывается нормально только в **Firefox**, в google chrome неправильный путь к картинкам.  
### --------------------------------------------------

# Домашнее задание: автотесты

Вам дано приложение на JavaScript и нужно написать для него автотесты: интеграционные тесты на интерфейс и модульные тесты на серверную часть.

## Предметная область

Приложение отображает в браузере информацию из git репозитория: список коммитов, файловую систему для выбранного коммита, содержимое выбранного файла (поддерживаются только текстовые форматы). Для удобства навигации на каджой странице отображаются "хлебные крошки".

## Как запустить

```sh
git clone git@github.com:dima117/shri-testing-homework.git
cd shri-testing-homework.git
npm i
npm start
```

## Интеграционные тесты

Сценарии для интеграционных тестов

- на всех страницах (история коммитов, просмотр файловой системы, просмотр содержимого файла) правильно отображается их содержимое;
- правильно работают переходы по страницам
  - из списка коммитов на список файлов
  - из списка файлов во вложенную папку
  - из списка файлов на страницу отдельного файла
  - переходы по хлебным крошкам

## Модульные тесты

- нужно добавить в README список логических блоков системы и их сценариев
- для каждого блока нужно написать модульные тесты
- если необходимо, выполните рефакторинг, чтобы реорганизовать логические блоки или добавить точки расширения
