---
title: Переполнение содержимого
slug: Learn_web_development/Core/Styling_basics/Overflow
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/CSS/Building_blocks/Handling_different_text_directions", "Learn/CSS/Building_blocks/Values_and_units", "Learn/CSS/Building_blocks")}}

В этом уроке мы рассмотрим другую важную концепцию в CSS — **переполнение**. Переполнение это то, что случается когда слишком много контента содержится внутри блока. В этом гайде вы изучите что это и как этим управлять.

| Необходимые условия: | Базовая компьютерная грамотность, [Установка базового ПО](/ru/docs/Learn_web_development/Getting_started/Environment_setup/Installing_software), базовые знания [работы с файлами](/ru/docs/Learn_web_development/Getting_started/Environment_setup/Dealing_with_files), основы HTML ([Введение в HTML](/ru/docs/conflicting/Learn_web_development/Core/Structuring_content)), и общее представление о том, как работает CSS (study [Введение в CSS](/ru/docs/conflicting/Learn_web_development/Core/Styling_basics).) |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Цель:                | Понять, что такое переполнение и как с ним работать.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

## Что такое переполнение?

Мы уже знаем, что всё в CSS — блоки, и что мы можем ограничивать размер этих блоков, присваивая им определённое значение посредством {{cssxref("width")}} и {{cssxref("height")}} (или {{cssxref("inline-size")}} и {{cssxref("block-size")}}). Переполнение — это то, что случается, когда у вас слишком много контента в блоке, так что он не помещается в данный ограниченный размер. CSS даёт нам различные инструменты для управления переполнением, и это также полезная концепция для понимания на этой ранней стадии. Вы будете встречаться с переполнением достаточно часто, когда пишите CSS, особенно когда глубже погрузитесь в CSS раскладку.

## CSS пытается избежать "потери данных"

Рассмотрим два примера, демонстрирующих поведение CSS по умолчанию при возникновении переполнения.

Первый пример — это блок, который был ограничен установленным параметром `height`. Затем мы добавили контент, превышающий выделенное пространство. Контент вышел за пределы поля и попал в абзац ниже.

{{EmbedGHLiveSample("css-examples/learn/overflow/block-overflow.html", '100%', 600)}}

Второй пример — слово в блоке. Блок оказался слишком маленьким для этого слова, и поэтому оно выходит за его пределы.

{{EmbedGHLiveSample("css-examples/learn/overflow/inline-overflow.html", '100%', 500)}}

Вы можете задаться вопросом, почему CSS работает так неаккуратно, отображая контент за пределами предназначенного для него блока. Почему бы не скрывать выходящий за пределы контент? Почему бы не масштабировать размер блока, чтобы он соответствовал размеру содержимого?

По возможности, CSS не скрывает контент, потому что это может привести к потере данных. Проблема состоит в том, что вы можете не заметить исчезновение данных. Посетители сайта тоже могут не заметить этого. Если кнопка отправки формы исчезнет и никто не может заполнить форму, это может стать большой проблемой! Поэтому, вместо того, чтобы скрывать выходящий за границы блока контент, CSS явно его отображает. Так вы с большей вероятностью увидите проблему при разработке. В худшем случае это заметит посетитель сайта и сообщит вам об этом.

Если вы ограничиваете поле с помощью параметров `width` или `height`, CSS доверяет вам и считает, что вы знаете, что делаете. CSS предполагает, что вы управляете ситуацией и предусматриваете возможность возникновения переполнения. В общем случае, ограничение размера блока проблематично, если он содержит текст. В этом месте может быть больше текста, чем вы ожидали или его размер может быть больше (например, если пользователь увеличил размер шрифта).

В следующих двух уроках объясняются различные подходы управления размерами, которые позволяют уменьшить вероятность возникновения переполнения. Однако, если вам нужен фиксированный размер блока, вы также можете контролировать поведение переполнения.

## Свойство overflow

Свойство {{cssxref("overflow")}} позволяет взять под контроль переполнение элемента и подсказать браузеру, как он должен себя вести. Значение overflow по умолчанию – `visible`, что означает - «показывать контент, когда он выходит за границы блока».

Чтобы обрезать контент выходящий за пределы блока, вы можете установить `overflow: hidden`. Это свойство делает именно то, о чём говорит: скрывает выходящий за пределы контент. Помните, что это может сделать часть содержимого невидимым. Используйте данное значение только в том случае, если скрытие содержимого не вызовет проблем.

{{EmbedGHLiveSample("css-examples/learn/overflow/hidden.html", '100%', 600)}}

Возможно, что при возникновении переполнения вместо скрытия вы захотите отобразить полосы прокрутки. При использовании `overflow: scroll` браузеры с видимыми полосами прокрутки всегда будут отображать их, даже если содержимого недостаточно для возникновения перекрытия. Это позволяет сохранить целостность раскладки, так как полосы прокрутки не будут появляться и пропадать в зависимости от количества содержимого в контейнере.

**Удалите часть содержимого из поля ниже. Обратите внимание, что полосы прокрутки остаются, даже если прокрутка не требуется.**

{{EmbedGHLiveSample("css-examples/learn/overflow/scroll.html", '100%', 600)}}

В приведённом выше примере нам нужно прокручивать содержимое только по оси `y`, однако мы получаем полосы прокрутки по обеим осям. Вы можете использовать свойство {{cssxref("overflow-y")}}, которое позволяет прокручивать содержимое только по оси `y`.

{{EmbedGHLiveSample("css-examples/learn/overflow/scroll-y.html", '100%', 600)}}

Вы также можете установить прокрутку по оси x с помощью {{cssxref("overflow-x")}}, но это не рекомендуемый способ отображения длинных слов! Если у вас есть длинное слово в маленьком поле, вы можете использовать свойства {{cssxref("word-break")}} или {{cssxref("overflow-wrap")}}. Кроме того, некоторые методы, описанные в разделе [Изменение размеров в CSS](/ru/docs/Learn_web_development/Core/Styling_basics/Sizing), могут помочь вам создавать блоки, которые лучше масштабируются с различным объемом содержимого.

{{EmbedGHLiveSample("css-examples/learn/overflow/scroll-x.html", '100%', 500)}}

Как и в случае со `scroll`, вы получаете полосу прокрутки независимо от того, достаточно ли содержимого для её появления.

> [!NOTE]
> Вы можете точно задать прокрутку по осям x и y, используя свойство `overflow`, передав два значения. Первое значение будет относиться к `overflow-x`, а второе — к `overflow-y`. Если передать одно значение, то `overflow-x` и `overflow-y` получат одинаковые значения. Например, `overflow: scroll hidden` устанавливает `overflow-x` в `scroll` и `overflow-y` в `hidden`.

Если вы хотите, чтобы полосы прокрутки отображались только тогда, когда содержимого больше, чем может поместиться в поле, используйте `overflow: auto`. Это позволяет браузеру автоматически определять, следует ли отображать полосы прокрутки.

**В приведённом ниже примере уменьшите количество содержимого так, чтобы оно поместилось в поле. Вы должны увидеть, что полосы прокрутки исчезнут.**

{{EmbedGHLiveSample("css-examples/learn/overflow/auto.html", '100%', 600)}}

## Overflow устанавливает контекст форматирования блока

Когда вы используете значение overflow, такое как `scroll` или `auto`, вы создаете **контекст форматирования блока** (BFC). Содержимое блока, для которого вы установили параметр `overflow` приобретает автономную раскладку. Контент вне блока не может проникнуть в блок, и ничто не может вылезти из этого блока в окружающее его пространство. Это дает возможность прокручивать содержимое, так чтобы оно не выходило за пределы блока.

## Нежелательное переполнение в веб-разработке

Современные методы раскладки (описанные в разделе [CSS раскладка](/ru/docs/Learn_web_development/Core/CSS_layout)) справляются с переполнением очень хорошо вне зависимости от того, сколько контента будет на веб-странице.

Это не всегда было нормой. В прошлом некоторые сайты были построены с блоками фиксированной высоты для выравнивания нижних границ блоков. Тем не менее эти блоки могли не иметь ничего общего между собой. Это была хрупкая конструкция. В устаревших приложениях вы можете встретить блок, в котором содержимое перекрывает другое содержимое на странице. Теперь вы понимаете, что это происходит из-за переполнения. В идеале вы должны провести рефакторинг разметки, чтобы не полагаться на блоки с фиксированной высотой.

При разработке сайта всегда помните о переполнении. Тестируйте дизайны как с большим, так и с малым количеством контента. Проверяйте различные размеры шрифта текстов. Убедитесь, что ваш CSS работает надёжно. Изменение значения overflow для скрытия содержимого или добавления полос прокрутки, должно использоваться только при необходимости (например там, где вы хотите использовать прокручиваемый блок).

## Проверьте свои навыки!

В этой статье мы рассмотрели многое, но можете ли вы вспомнить самую важную информацию? Вы можете найти дополнительные тесты, чтобы убедиться, что вы усвоили эту информацию, прежде чем двигаться дальше – см. [Проверь свои навыки: переполнение](/ru/docs/Learn/CSS/Building_blocks/Overflow_Tasks).

## Заключение

В этом уроке была представлена концепция переполнения. Важно понимать, что CSS по умолчанию старается избежать обрезания выходящего за границы блока содержимого. Мы изучили, как можно справиться с возникшим переполнением, а также рассмотрели важность тестирования поведения веб-страниц как с малым количеством контента, так и с большим.

{{PreviousMenuNext("Learn/CSS/Building_blocks/Handling_different_text_directions", "Learn/CSS/Building_blocks/Values_and_units", "Learn/CSS/Building_blocks")}}

## In this module

1. [Каскад и наследование](/ru/docs/Learn_web_development/Core/Styling_basics/Handling_conflicts)
2. [Селекторы CSS](/ru/docs/Learn_web_development/Core/Styling_basics/Basic_selectors)
   - [Селекторы типа, класса и ID](/ru/docs/conflicting/Learn_web_development/Core/Styling_basics/Basic_selectors)
   - [Селекторы атрибута](/ru/docs/Learn_web_development/Core/Styling_basics/Attribute_selectors)
   - [Псевдоклассы и псевдоэлементы](/ru/docs/Learn_web_development/Core/Styling_basics/Pseudo_classes_and_elements)
   - [Комбинаторы](/ru/docs/Learn_web_development/Core/Styling_basics/Combinators)

3. [Блочная модель(The box model)](/ru/docs/Learn_web_development/Core/Styling_basics/Box_model)
4. [Фон и границы](/ru/docs/Learn_web_development/Core/Styling_basics/Backgrounds_and_borders)
5. [Обработка разных направлений текста](/ru/docs/Learn_web_development/Core/Styling_basics/Handling_different_text_directions)
6. [Переполнение содержимого](/ru/docs/Learn_web_development/Core/Styling_basics/Overflow)
7. [Значения и единицы измерения](/ru/docs/Learn_web_development/Core/Styling_basics/Values_and_units)
8. [Размеры в CSS](/ru/docs/Learn_web_development/Core/Styling_basics/Sizing)
9. [Элементы изображений, форм и медиа-элементы](/ru/docs/Learn_web_development/Core/Styling_basics/Images_media_forms)
10. [Стилизация таблиц](/ru/docs/Learn_web_development/Core/Styling_basics/Tables)
11. [Отладка CSS](/ru/docs/Learn_web_development/Core/Styling_basics/Debugging_CSS)
12. [Организация вашей CSS](/ru/docs/Learn/CSS/Building_blocks/Organizing)
