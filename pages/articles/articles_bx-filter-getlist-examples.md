---
title: Статьи 1С | Примеры фильтра для GetList и компонентов
keywords: фильтры в битрикс, getlist filter
sidebar: articles_sidebar
folder: articles
permalink: articles_bx-filter-getlist-examples.html
summary: Примеры часто используемых настроек при фильтрации элементов, сслыки на статьи и документацию по работе фильтров и с фильтрами в Битрикс
toc: false
---

## Примеры фильтра для GetList и компонентов

**Дополнительные ссылки:**

* [https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=43&LESSON_ID=2683#types](https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=43&LESSON_ID=2683#types)

#### Варианты модификаторов условий фильтрации

  * ```!``` - отрицание;
  * ```+``` - значения null, 0 и пустая строка так же удовлетворяют условиям фильтра.
  * ```>=``` - значение поля больше или равно передаваемой в фильтр величины;
  * ```>``` - значение поля строго больше передаваемой в фильтр величины;
  * ```<=``` - значение поля меньше или равно передаваемой в фильтр величины;
  * ```<``` - значение поля строго меньше передаваемой в фильтр величины;
  * ```@``` - оператор может использоваться для целочисленных и вещественных данных при передаче набора значений (массива). В этом случае при генерации sql-запроса будет использован sql-оператор IN, дающий компактную форму записи;
  * ```~``` - значение поля проверяется на соответствие передаваемому в фильтр шаблону;
  * ```%``` - значение поля проверяется на соответствие передаваемой в фильтр строке в соответствии с языком запросов.

### Убрать из выдачи товары БЕЗ изображений

```php
$arrFilterSearch = [
	'!PREVIEW_PICTURE' => false,
];
```

### Убрать из выдачи товары БЕЗ цены (по типу цен)

```php
// не забываем выносить все значимые данные 
// в файл констант /local/php_interface/include/constants.php

define("PRICE_ROZNICA_ID", 47);

$arrFilterSearch = [
	'>CATALOG_PRICE_'.PRICE_ROZNICA_ID => '0',
];
```

### Фильтруем данные по условию "ИЛИ"

```php

// Получим товары у которых свойство TSENA_DO_AKTSII пусто или меньше 0
$arrFilterSearch = [
	[
		"LOGIC" => "OR",
		['PROPERTY_TSENA_DO_AKTSII' => false],
		['<PROPERTY_TSENA_DO_AKTSII_VALUE' => 0],
	]
];
```