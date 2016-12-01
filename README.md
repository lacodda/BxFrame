# BxFrame

## Bitrix Module

API для сборки кастомных админок в Битриксе

Документация по модулю доступна по адресу [http://api.digitalwand.ru/admin_helper/](http://api.digitalwand.ru/admin_helper/). Её же можно прочитать в комментариях в коде модуля. 

Простой рабочий пример реализован отдельным модулем 
[lacodda.bxmodule-demo](https://github.com/Lacodda/lacodda.bxmodule-demo)

## Концепция
Данный модуль реализует подход MVC для создания административного интерфейса.

Возможность построения административного интерфейса появляется благодаря наличию единого API для CRUD-операциями над
сущностями. Поэтому построение админ. интерфейса средствами данного модуля возможно только для классов, реализующих
API ORM Битрикс. При желании использовать данный модуль для сущностей, не использующих ORM Битрикс, можно
подготовить для таких сущностей класс-обёртку, реализующий необходимые функции.

Основные понятия модуля:
<ul>
<li>Модель: "model" в терминах MVC. Класс, унаследованный от DataManager или реализующий аналогичный API.</li>
<li>Хэлпер: "view" в терминах MVC. Класс, реализующий отрисовку интерфейса списка или детальной страницы.</li>
<li>Роутер: "controller" в терминах MVC. Файл, принимающий все запросы к админке данного модуля, создающий нужные
хэлперы с нужными настройками. С ним напрямую работать не придётся.</li>
<li>Виджеты: "delegate" в терминах MVC. Классы, отвечающие за отрисовку элементов управления для отдельных полей
сущностей. В списке и на детальной.</li>
</ul>

Схема работы с модулем следующая:
<ul>
<li>Реализация класса AdminListHelper - для управления страницей списка элементов</li>
<li>Реализация класса AdminEditHelper - для управления страницей просмотра/редактирования элемента</li>
<li>Создание файла Interface.php с вызовом AdminBaseHelper::setInterfaceSettings(), в которую передается
конфигурация
полей админки и классы, используемые для её построения.</li>
<li>Если не хватает возможностей виджетов, идущих с модулем, можно реализовать свой виджет, унаследованный от любого
другого готового виджета или от абстрактного класса HelperWidget</li>
</ul>

Рекомендуемая файловая структура для модулей, использующих данный функционал:
<ul>
<li>Каталог <b>admin</b>. Достаточно поместить в него файл menu.php, отдельные файлы для списка и детальной
создавать не надо благодаря единому роутингу.</li>
<li>Каталог <b>classes</b> (или lib): содержит классы модели, представлений и делегатов.</li>
<li> -- <b>classes/helper</b>: каталог, содержащий классы "view", унаследованные от AdminListHelper и
AdminEditHelper.</li>
<li> -- <b>classes/widget</b>: каталог, содержащий виджеты ("delegate"), если для модуля пришлось создавать
свои.</li>
<li> -- <b>classes/model</b>: каталог с моделями, если пришлось переопределять поведение стандартных функций getList
и т.д.</li>
</ul>

Использовать данную структуру не обязательно, это лишь рекомендация, основанная на успешном опыте применения модуля
в ряде проектов.

## Bitrix Console

[![Build Status](https://travis-ci.org/lacodda/bitrix-cli.svg)](https://travis-ci.org/lacodda/bitrix-cli)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/lacodda/bitrix-cli/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/lacodda/bitrix-cli/?branch=master)
[![Latest Stable Version](https://poser.pugx.org/lacodda/bitrix-cli/v/stable)](https://packagist.org/packages/lacodda/bitrix-cli) 
[![Total Downloads](https://poser.pugx.org/lacodda/bitrix-cli/downloads)](https://packagist.org/packages/lacodda/bitrix-cli) 
[![License](https://poser.pugx.org/lacodda/bitrix-cli/license)](https://packagist.org/packages/lacodda/bitrix-cli)

Console application for administration and support projects on Bitrix CMS. 

Features:

* Continuous integration.
* Environments settings.
* Managing caching, modules, search system.
* Nice API for creating agents.

Made based on Symfony Console ♥.

## Installation

```bash
composer require lacodda/bxframe

./vendor/bin/bxcli init
```

## Documentation

* [По-русски](docs/ru/README.md)