BEM: Key concepts
=================

-   [Block](#Блок)
-   [Element](#Элемент)
-   [Modifier](#Модификатор)
-   [BEM entity](#БЭМ-сущность)
-   [Mixin](#Микс)
-   [BEM tree](#БЭМ-дерево)
-   [Block implementation](#Реализация-блока)
-   [Block implementation technology](#Технология-реализации)
-   [Block redefinition](#Переопределение-блока)
-   [Redefinition level](#Уровень-переопределения)

<a name="block"></a>

Block
-----

A logically and functionally independent page component, the equivalent of a component in Web Components. A block encapsulates behavior (JavaScript), templates, styles (CSS), and other [implementation technologies](#Технология-реализации). Blocks being independent allows for their re-use, as well as facilitating the [project development and support process](../solved-problems/solved-problems.en.md).

#### Block features

**Nested structure**

Blocks can be nested inside any other blocks.

For example, a `head` block can include a logo (`logo`), a search form (`search`), and an authorization block (`auth`).

![Head block components](https://img-fotki.yandex.ru/get/15534/158800653.0/0_111fb2_7710ab3d_orig)

**Arbitrary placement**

Blocks can be moved around on a page, moved between pages or projects. The implementation of blocks as independent entities makes it possible to change their position on the page and ensures their proper functioning andappearance.

Thus, the logo and the authorization form can be swapped around withoutmodifying the blocks' CSS or JavaScript code.

![Altering the blocks' positions](https://img-fotki.yandex.ru/get/16156/158800653.0/0_111fb3_2fec3fed_orig)

![Altering the blocks' positions](https://img-fotki.yandex.ru/get/15542/158800653.0/0_111fb1_bcbc3c6a_orig)

**Re-use**

An interface can contain multiple instances of the same block.

![Online store products](https://img-fotki.yandex.ru/get/15498/158800653.0/0_111fb0_fbb195e9_orig)

Element
-------

A constituent part of a [block](#Блок) that can't be used outside of it.

For example, a menu item is not used outside of the context of a menu block,therefore it is an element.

![Menu items](https://img-fotki.yandex.ru/get/15588/158800653.0/0_111fb6_192672cf_orig)

> [A block or an element: when should I use which?](../../faq/faq.en.md#В-каком-случае-создавать-блок-в-каком-элемент)

> [Why does the BEM methodology not allow elements within elements?](../../faq/faq.en.md#Почему-в-БЭМ-не-рекомендуется-создавать-элементы-элементов-block__elem1__elem2)

Modifier
--------

A BEM entity that defines the appearance and behavior of a [block](#Блок) or an [element](#Элемент).

The use of modifiers is optional.

Modifiers are similar in essence to HTML attributes. The same block looksdifferent due to the use of a modifier.

For instance, the appearance of the menu block (`menu`) may change depending on a modifier that is used on it.

![Add a menu to the footer](https://img-fotki.yandex.ru/get/16183/158800653.0/0_111fba_921b3c47_orig)

BEM entity
----------

[Blocks](#Блок), [elements](#Элемент), and [modifiers](#Модификатор) are all called BEM entities.

It is a notion that can be used both to refer to an individual BEM entityand as a generic term for blocks, elements, and modifiers.

Mixin
-----

An instance of different [BEM entities](#БЭМ-сущность) being hosted on a single [DOM node](https://en.wikipedia.org/wiki/Document_Object_Model).

Mixins allow us to:

-   combine the behaviors and styles of several BEM entities while avoiding codeduplication;
-   create semantically new interface components on the basis of existing BEMentities.

Let's consider the case of a mixin comprising a block and an element ofanother block.

Let's assume that links in your project are implemented via a `link` block. We need to format menu items as links. There are several ways to do that:

-   Create a modifier for a menu item that turns the item into a link. Implementing such a modifier would necessarily involve copying the behavior and styles of the `link` block. That would result in code duplication.

-   Have a mixin combining a generic `link` block and a `link` element of a `menu` block. A mixin of the two BEM entities will allow us to use the basic link functionality of the `link` block and additional CSS rules of the `menu` block without copying the code.

BEM tree
--------

A representation of a web page structure in terms of blocks, elements, and modifiers. It is an abstraction over a [DOM tree](https://en.wikipedia.org/wiki/Document_Object_Model) that describes the names of BEM entities, their states, order, nesting, and auxiliary data.

In real-life projects, a BEM tree can be presented in any format that supportsthe tree structure.

Let's consider an example of a DOM tree:

``` html
<header class="header"> <img class="logo"> <form class="search"> <input type="input"> <button type="button"></button> </form> <div class="lang-switcher"></div> </header>
```

The corresponding BEM tree will look like this:

    header ├──logo └──search ├──input └──button └──lang-switcher

In XML and [BEMJSON](https://en.bem.info/technology/bemjson/current/bemjson/) formats, the same BEM tree will appear as follows:

XML

``` xml
<block:header> <block:logo/> <block:search> <block:input/> <block:button/> </block:search> <block:lang-switcher/></block:header>
```

BEMJSON

``` js
{ block: 'header', content : [ { block : 'logo' }, { block : 'search-form', content : [ { block : 'input' }, { block : 'button' } ] }, { block : 'lang-switcher' } ]}
```

Block implementation
--------------------

A set of different [technologies](#Технология-реализации) that determine the following aspects of a BEM entity:

-   behavior;
-   appearance;
-   tests;
-   templates;
-   documentation;
-   description of dependencies;
-   additional data (e.g., images).

Implementation technology
-------------------------

A technology used for [implementing](#Реализация-блока) a block.

Blocks can be implemented in one or more technologies, for example:

-   behavior — JavaScript, CoffeeScript;
-   appearance — CSS, Stylus, Sass;
-   templates — BEMHTML, BH, Jade, Handlebars, XSL;
-   documentation — Markdown, Wiki, XML.

For instance, if the appearance of a block is defined with CSS, that meansthat the block is implemented in the CSS technology. Likewise, if the documentation for a block is written in MarkDown format, the block is implemented in the MarkDown technology.

### Block redefinition

Modifying a block [implementation](#Реализация-блока) by adding new features to the block on a different [level](#Уровень-переопределения).

Redefinition level
------------------

A set of BEM entities and their partial [implementations](#Реализация-блока).

The final implementation of a block can be divided into different redefinition levels. Each new level extends or overrides the block's original implementation. The end result is assembled from individual [implementation technologies](#Технология-реализации-блока) of the block from all redefinition levels in a pre-determined consecutive order.

Any [implementation](#Технология-реализации-блока) technologies of BEM entities can be [redefined](#Переопределение-блока).

For example, there is a third-party library linked to a project on a separatelevel. The library contains ready-made block implementations. The project-specific blocks are stored on a different redefinition level.

Let's say we need to modify the appearance of one of the library blocks. That doesn't require changing the CSS rules of the block in the library source code or copying the code at the project level. We only need to create additional CSS rules for that block at the project level. During the build process, the resulting implementation will incorporate both the original functionality from the library level and the new styles from the project level.
