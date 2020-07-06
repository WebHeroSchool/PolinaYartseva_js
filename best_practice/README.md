// 1. Используйте пробелы вместо табуляции

// Плохо
function foo() {
∙∙∙∙let name;
}

// Хорошо
function baz() {
∙∙let name;
}

// 2. Точки с запятыми необходимы

// Плохо
let luke = {}
let leia = {}
[luke, leia].forEach(jedi => jedi.father = ‘vader’)

// Хорошо
let luke = {};
let leia = {};
[luke, leia].forEach((jedi) => {
jedi.father = ‘vader’;
});

// 3. Больше не используйте var

// Плохо
var example = 42;

// Хорошо
let example = 42;

//4. Стрелочные функции предпочтительнее

// Плохо
[1, 2, 3].map(function (x) {
const y = x + 1;
return x * y;
});

// Хорошо
[1, 2, 3].map((x) => {
const y = x + 1;
return x * y;
});

//5. Используйте шаблонные строки вместо объединения

// Плохо
function sayHi(name) {
return ‘How are you, ‘ + name + ‘?’;
}

// Плохо
function sayHi(name) {
return [‘How are you, ‘, name, ‘?’].join();
}

// Хорошо
function sayHi(name) {
return `How are you, ${name}?`;
}

//6. Не используйте eval()

// Плохо
let obj = { a: 20, b: 30 };
let propName = getPropName(); // returns “a” or “b”
eval( ‘var result = obj.’ + propName );

// Хорошо
let obj = { a: 20, b: 30 };
let propName = getPropName(); // returns “a” or “b”
let result = obj[ propName ]; // obj[ “a” ] is the same as obj.a

//7. По переменной на объявление
     
// Плохо
let a = 1, b = 2, c = 3;

// Хорошо
let a = 1;
let b = 2;
let c = 3;

//8. Не используйте нижнее подчеркивание в начале или конце названий.

//Плохо
let name_ = 'Max';
foo._bar();

//Хорошо
let name = 'Max';
foo.bar();

//9. Не нужно неинициализированной переменной задавать значение undefined, это значение присваивается автоматически.

//Плохо
let foo = undefined;
let bar = undefined;

//Хорошо
let foo;
let bar;

//10. При использовании конструкции if .. else располагайте else на одной строке со скобкой закрывающей блок if.

//Плохо
if (test) {
  thing1();
  thing2();
}
else {
  thing3();
}

//Хорошо
if (test) {
  thing1();
  thing2();
} else {
  thing3();
}