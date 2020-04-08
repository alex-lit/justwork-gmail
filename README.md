# Представьте, что вам необходимо реализовать front-приложение для сервиса Gmail.

## Разбиение на компоненты

Интерфейс

![main](https://raw.githubusercontent.com/alex-lit/justwork-gmail/master/images/1.png)

Содержимое

![mail](https://raw.githubusercontent.com/alex-lit/justwork-gmail/master/images/3.png)

Разбиение на компоненты предварительное, как правило со временем компонент
разрастается и разделяется на несколько более мелких.

> Подразумевается что такие компоненты как кнопки, чекбоксы, селекты и т.д. уже
> вынесены в UI-библиотеку и берутся из нее.

## Структура файлов проекта

```plaintext
[api] // слой работы с API
  index.ts // экспортирует сущности для дальнейшей реализации доступа к ним через плагин (./plugins/api.ts)
  [entities] // сущности, например user, account, mail и т.д.
    [entity-1]
      index.ts
    [entity-2]
    ...

[assets] // ресурсы обрабатываемые сборщиком
  [fonts]
  [media]
    [images]
    [videos]
    [audios]
    ...
  [styles]
  ...

[components] // компоненты
  [component-1] // директория компонента
    [assets] // структура аналогичнa [assets] в корне  (опционально)
    [locales] // структура аналогичнa [locales] в корне (опционально)
    [components] // дочерние компоненты (опционально)
      [supcomponent-1]
        supcomponent-1.spec.ts
        supcomponent-1.component.ts
        index.ts
      [supcomponent-2]
      ...
    component-1.spec.ts // unit тест
    component-1.component.vue // SFC
    index.ts
  [component-2]
  ...

[layouts] // шаблоны страниц
  layout-1.vue
  layout-2.vue
  ...

[locales] // словари локализации
  ru.(json|yaml)
  en.(json|yaml)
  ...

[middleware] // функции выполняемые перед переходом по страницам
  middleware-1.ts
  middleware-2.ts
  ...

[pages] // страницы
  [page-1]
    [subpage-1]
      index.vue
    [subpage-2]
    ...
    index.vue
  [page-2]
  ...

[plugins] // плагины Vue.js и их конфиги
  [plugin-1] // директория плагина можен содержать отдельные утилиты, миксины для vue-компонент и т.д.
    [mixins]
    [utils]
    ...
    plugin-1.plugin.ts
    index.ts
  [plugin-2]
  ...

[static] // статические ресурсы (robots.txt, иконки и т.д)
  robots.txt
  manifest.json
  ...

[store] // модули состояния приложения (Vuex)
  [module-1]
    index.ts
    [submodule-1]
      index.ts
    [submodule-2]
    ...
  [module-2]
  ...
  index.ts // корневой уровень

[utils] // утилиты
  [util-1]
    util-1.spec.ts
    util-1.util.ts
    index.ts
  [util-2]
  ...
  index.ts // экспорт утилит
```

## Именование файлов и каталогов

Файлы и каталоги именуются в kebab-case. Имя компонента состоит из 2х-3х слов
для сохранения консистентности с HTML, где стандартные теги из одного слова, а
веб-компоненты - из 2х и более.

Пример:

```html
<!-- стандартный тег -->
<section class="demo">
  <!-- комонент -->
  <my-component>
    <!-- комонент -->
    <sub-component></sub-component>
    <!-- /комонент -->
  </my-component>
  <!-- /комонент -->
</section>
<!-- /стандартный тег -->
```

## Приоритеты создания компонент/страниц

Страница представляет из себя компоновку компонент.

Помимо компонент страница содержит данные для секции "head" html-документа и
может принимать данные с сервера для передачи их в компоненты.
