## Примеры кода на JavaScript

Question: What is the value of foo?
~~~~
var foo = 10 + '20';
~~~~
Ответ: '1020'. Приведение типов преобразует 10 в строку и сложит 2 строки.


Question: What will be the output of the code below?
~~~~
console.log(0.1 + 0.2 == 0.3);
~~~~
Ответ: false. Из-за плавающей точки результатом вычисления будет 0.30000000000000004. Чтобы справится с этой проблемой нужно округлять числа до десятков.


Question: How would you make this work?
~~~~
add(2, 5); // 7
add(2)(5); // 7
~~~~
Ответ:
~~~~
function add(a, b) {
  return a && b ? a + b : function (c) { return a + c; };
}
~~~~


Question: What value is returned from the following statement?
~~~~
"i'm a lasagna hog".split("").reverse().join("");
~~~~
Ответ: `'goh angasal a m\'i'`


Question: What is the value of window.foo?
~~~~
( window.foo || ( window.foo = "bar" ) );
~~~~
Ответ: 'bar'


Question: What is the outcome of the two alerts below?
~~~~
var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);
~~~~
Ответ:
1. `Hello World` из функции.
2. `ReferenceError: bar is not defined` т.к переменная `bar` бар определена в области видимости функции и не видна за ее пределами. 


Question: What is the value of foo.length?
~~~~
var foo = [];
foo.push(1);
foo.push(2);
~~~~
Ответ: 2;


Question: What is the value of foo.x?
~~~~
var foo = {n: 1};
var bar = foo;
foo.x = foo = {n: 2};
~~~~
Ответ: `undefined`. 
`foo.x = foo = {n: 2}` то же, что и `foo.x = (foo = {n: 2})`. `foo` на которую ссылается `foo.x` "устанавливается" перед тем, как `foo` изменится. `foo.x` ссылается на старое значение `foo`. Это значит, что в старом `foo` появится новое свойство `x` равное `{n: 2}`. А в новое `foo` запишется `{n: 2}`. Значение старого `foo` находится в `bar`.
~~~~
{
  n: 1,
  x: {
    n: 2
  }
}
~~~~
Так как при дальнейшем выводе `foo.x` наше `foo` ссылается на его новое значение, в котором отстутствует `x`, то `foo.x` будет неопределено.


Question: What does the following code print?
~~~~
console.log('one');
setTimeout(function() {
  console.log('two');
}, 0);
Promise.resolve().then(function() {
  console.log('three');
})
console.log('four');
~~~~
Ответ: 'one', 'four', 'three', 'two'. `setTimeout` часть основной очереди (main task queue), тогда как `Promise` в miscro task queue, которая выполняется перед основной. Поэтому сначала выведентся 'three', а потом 'two'.


Question: What is the difference between these four promises?
~~~~
doSomething().then(function () {
  return doSomethingElse();
});
doSomething().then(function () {
  doSomethingElse();
});
doSomething().then(doSomethingElse());
doSomething().then(doSomethingElse);
~~~~

[Подробный ответ](http://frontiermag.ru/problem-with-promises.html)