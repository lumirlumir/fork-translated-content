---
title: Логическое нулевое присваивание (??=)
slug: Web/JavaScript/Reference/Operators/Nullish_coalescing_assignment
---

{{jsSidebar("Operators")}}

Оператор логического нулевого присваивания (`x ??= y`) присваивает значение переменной `x`, если она содержит {{Glossary("nullish", "похожее на null значение")}} (`null` или `undefined`).

{{InteractiveExample("JavaScript Demo: Expressions - Nullish coalescing assignment")}}

```js interactive-example
const a = { duration: 50 };

a.speed ??= 25;
console.log(a.speed);
// Expected output: 25

a.duration ??= 10;
console.log(a.duration);
// Expected output: 50
```

## Синтаксис

```js-nolint
x ??= y
```

## Описание

### Сокращённое вычисление

Оператор [нулевого слияния](/ru/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing) вычисляется слева направо, делая возможным сокращённое вычисление выражения, согласно следующему правилу:

`(выражение без null или undefined) ?? следующее выражение` останавливает вычисление на левом выражении, если его результат отличен от `null` или `undefined`.

Сокращённое вычисление означает, что `следующее выражение` **не будет вычислено**, соответственно не будет никаких последствий, связанных с ним (например, если `следующее выражение` содержит вызов функции, то он никогда не произойдёт).

Логическое нулевое присваивание также поддерживает сокращённое вычисление, поэтому `x ??= y` по сути то же самое, что и выражение ниже:

```js
x ?? (x = y);
```

В отличие от следующего примера, где операция присваивания произойдёт вне зависимости от результата вычисления:

```js example-bad
x = x ?? y;
```

## Примеры

### Использование логического нулевого присваивания

```js
function config(options) {
  options.duration ??= 100;
  options.speed ??= 25;
  return options;
}

config({ duration: 125 }); // { duration: 125, speed: 25 }
config({}); // { duration: 100, speed: 25 }
```

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- [Оператор нулевого слияния (`??`)](/ru/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing)
- {{Glossary("Nullish", "Похожее на null значение")}}
- {{Glossary("Truthy", "Истиноподобное значение")}}
- {{Glossary("Falsy", "Ложноподобное значение")}}
