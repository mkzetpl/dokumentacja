# JS

## Okna dialogowe

```js
alert('treść komunikatu'); // OK - nic nie zwraca
confirm('treść komunikatu'); // OK - true, ANULUJ - false
prompt('treść komunikatu', 'domyślna wartość'); // ANULUJ - false, OK - wpisana wartość
```

## Zmienne

### Deklaracja zmiennych

```js
var a = 20; // nie zalecane w użyciu, zasięg funkcyjny
let b = 20; // zasięg blokowy
const c = 20; // stała, zasięg blokowy
```

### Typy zmiennych

```js
// Typy proste:
let firstName = 'Jan'; //string
let year = 2018; //number
let isDelete = true; //boolean
let lastName; //undefined
let fullName = undefined; //undefined
let nothing = null; //null
let Sym1 = Symbol('Sym'); // symbol

const najwiekszyInt = 9007199254740991n // BigInt jest tworzony przez dodanie n na końcu literału liczby
const duzyString = BigInt('9007199254740991'); // przez wywołanie funkcji BigInt()


// Typy złożone
Object (w tym Array, Map i Set)

// nie mają przypisanej bezpośrednio wartości,
// tylko wskazują na miejsce w pamięci,
// gdzie te dane są przetrzymywane.
const a = [1, 2, 3];
const b = a;
a.push(4);
console.log(a); //[1, 2, 3, 4]
console.log(b); //[1, 2, 3, 4]

const a = { name : "kot" }
const b = a;
const c = b;
const d = c;
d.name = "pies";
console.log(a, b, c, d); { name : "pies" } { name : "pies" } { name : "pies" } { name : "pies" }

// typy proste są niemutowalne
// typy złożone przeciwnie
const tab = [1, 2, 3, 4]; //tablica - obiekt złożony
tab[0] = "kot";
console.log(tab); //["kot", 2, 3, 4]; //zmieniłem pierwszy klucz

//typ prosty
const txt = "Ala ma kota";
txt[0] = "O"; //spróbuję zmienić pierwszą literę
console.log(txt); //Ala ma kota

// przy pracy z typami prostymi działamy
// na tym co zwróci dana funkcja,
// a nie modyfikujemy bezpośrednio danej wartości:

const txt = "ala";
const big = txt.toUpperCase(); //funkcja toUpperCase() zwróciła tekst pisany dużymi literami

console.log(big); //"ALA"
console.log(txt); //"ala"
```

### Sprawdzanie typu danych

```js
const nr = 10;
const txt = 'przykładowy tekst';
const arr = [1, 2, 3];
const ob = {};
const n = null;
//zmiennej zzz specjalnie nie zadeklarowana

console.log(typeof nr); //"number"
console.log(typeof txt); //"string"
console.log(typeof arr); //"object" hmm?
console.log(typeof ob); //"object"
console.log(typeof n); //"object" hmm?
console.log(typeof zzz); //"undefined"

// sprawdzenie typu zmiennych
if (typeof nr === "number") {...}
if (typeof txt === "string") {...}
if (Array.isArray(arr)) {...}
if (typeof ob === "object") {...}
if (n === null) {...}
if (typeof zzz === "undefined") {...}
```

### Operacje na różnych typach

```js
'1' + 2; //"12"
2 + '1'; //"21"

2 + 3 + '4'; //"54" ponieważ 2+3=5 czyli 5 + "4"
2 + 2 + 3 + '3'; //"73"
2 + 2 + '3' + 3; //"433"

'2' * 3; //6
3 * '3'; //9
'5' - 1; //4
8 / '2'; //4

//  ------------------------ ZOSTAWIĆ CZY WYRZUCIĆ ???? ----------------------
[1, 2, 3] + "kot" //1,2,3kot, bo tablica została skonwertowana na 1,2,3
23 + "" + false  //"23false"

[] + "kot"  //"kot", bo tablica została skonwertowana na ""
[]  + []  //"", bo obie tablice zostały skonwertowane na "" czyli mamy "" + ""
[] + false  //"false"

"" + {}  //"[object Object]" bo obiekt został skonwertowany na zapis [object Object]
[1, 2, 3] + {}  //"1,2,3[object Object]"
{} + {}  //"[object Object][object Object]"
"23" + [1, 2, 3] + {} + !true  //"231,2,3[object Object]false"

null + null //0
null + true //1
null + true + "10" //"110"
//  ------------------------ ZOSTAWIĆ CZY WYRZUCIĆ ???? ----------------------
```

### Ręczna konwersja danych

```js
// konwersja danych na string
const nr = 102;

console.log('' + nr); // "102"
console.log(nr.toString()); // "102"
console.log(String(nr)); // "102"

String(102); //"102"
String(true); //"true"
String(null); //"null"
String(undefined); //"undefined"

// konwersja na liczbę
// Number(), parseInt(), parseFloat();
console.log(Number('100')); // 100
console.log(Number('50.5')); // 50.5
console.log(Number('50px')); // NaN

console.log(parseInt('24px', 10)); // 24
console.log(parseInt('26.5', 10)); // 26
console.log(parseInt('100kot', 10)); // 100
console.log(parseInt('Ala102', 10)); // NaN - zaczyna się od liter
console.log(parseInt('Hello', 10)); // NaN
console.log(parseInt('1000', 2)); // 8

// Różnica pomiędzy parseFloat() a funkcją Number()
//  jest taka, że pierwsza z nich na końcu tekstu
// ignoruje wszystkie znaki niebędące poprawnym
// zapisem liczbowym, a druga - tylko białe znaki.
console.log(parseFloat('26.5px', 10)); // 26.5
console.log(parseFloat('10')); // 10
console.log(parseFloat('10.00')); // 10
console.log(parseFloat('10.33')); // 10.33
console.log(parseFloat('34 45 66')); // 34
console.log(parseFloat('   60   ')); // 60
console.log(parseFloat('40 years')); // 40
console.log(parseFloat('He was 40')); // NaN

// toFixed(digits)
// zwraca tekst będący liczbą zapisaną z daną precyzją.
// Parametr digits określa liczbę cyfr po przecinku
const nr = 123.456789;

nr.toFixed(); // "123"
nr.toFixed(0); // "123"
nr.toFixed(1); // "123.5"
nr.toFixed(2); // "123.46"
nr.toFixed(3); // "123.457"
nr.toFixed(4); // "123.4568"
nr.toFixed(5); // "123.45679"
nr.toFixed(6); // "123.456789"
nr.toFixed(7); // "123.4567890"
nr.toFixed(8); // "123.45678900"
nr.toFixed(9); // "123.456789000"
nr.toFixed(10); // "123.4567890000"
nr.toFixed(11); // "123.45678900000"

// toPrecision(digits)
// parametr digits, który określa liczbę cyfr
// w całym zapisie musi być z przedziału 1-100

nr.toPrecision(); // "123.456789"
nr.toPrecision(0); // błąd, parametr musi być z przedziału 1-100
nr.toPrecision(1); // "1e+2"
nr.toPrecision(2); // "1.2e+2"
nr.toPrecision(3); // "123"
nr.toPrecision(4); // "123.5"
nr.toPrecision(5); // "123.46"
nr.toPrecision(6); // "123.457"
nr.toPrecision(7); // "123.4568"
nr.toPrecision(8); // "123.45679"
nr.toPrecision(9); // "123.456789"
nr.toPrecision(10); // "123.4567890"
nr.toPrecision(11); // "123.45678900"

// Boolean()
Boolean(102); //true
Boolean('kot'); //true

Boolean(false); //false
Boolean(null); //false
Boolean(undefined); //false
Boolean(0); //false
Boolean(NaN); //false
Boolean(''); //false
Boolean(document.all); //false
```

# Operatory

### Operatory dodawania, odejmowania, mnożenia, dzielenia

```js
const x = 5;
console.log(x + 2); //7
console.log(x - 1); //4
console.log(x * 3); //15
console.log(x / 2); //2.5

//% - modulo czyli reszta z dzielenia
console.log(x % 2); //1
console.log(9 % 3); //0

//** - potęgowanie
console.log(x ** 2); //25 - równoznaczne z Math.pow(x, 2)
console.log(3 ** 3); //27 - równoznaczne z Math.pow(3, 3)
```

### Operatory przypisania

```js
let x = 5;
x += 3; // równoznaczne z x = x + 3;
x -= 3; // równoznaczne z x = x - 3;
x *= 3; // równoznaczne z x = x * 3;
x /= 3; // równoznaczne z x = x / 3;
x %= 3; // równoznaczne z x = x % 3;
x++; // równoznaczne z x = x + 1; zwiększenie w następnej instrukcji
x--; // równoznaczne z x = x - 1; zmniejszenie w nast epnej instrukcji
++x; // zwiększona w danej instrukcji
--x; // zmniejszona w danej instrukcji

// ------ Przykład  inkrementacji i dekrementacji ------
let x = 5;
console.log(x++); //5
console.log(x); //6

let y = 5;
if (y-- < 5) {
   //nie zadziała
   console.log(y); //4
}

let x = 5;
console.log(++x); //6
console.log(x); //6

let y = 5;
if (--y < 5) {
   //zadziała
   console.log(y); //4
}
```

### Operatory porównania

```js
//== - porównuje obie wartości
let a = 10;
let b = 20;
console.log(a == b); //false;
console.log(a == 10); //true

//=== - porównuje obie wartości i ich typ
let a = 10;
let b = '10';
console.log(a === 20); //false
console.log(a == b); //true
console.log(a === b); //false

//!= - czy wartości są różne
let a = 10;
let b = 20;
console.log(a != b); //true
console.log(a != '10'); //false

//!== - czy wartości są różne. W przypadku różnych typów zawsze zwróci false
let a = 10;
let b = 20;
console.log(a !== b); //true
console.log(a != '10'); //false
console.log(a !== '10'); //true

//< i > - mniejsze i większe
let a = 10;
let b = 20;
console.log(a < b); //true
console.log(a > b); //false

//<= i >= - mniejsze-równe i większe-równe
let a = 10;
let b = 20;
let c = 10;
console.log(a <= b); //true
console.log(a <= c); //true
```

### Operatory logiczne

```js
&& // and (i)
|| // or (lub)
^ // xor (jeden z, ale nie dwa równocześnie)
! // not (negacja)

//&& - operator "i" - wszystkie warunki muszą być spełnione
let x = 6;
let y = 3;
console.log(x > 3 && y > 3); //false bo drugie równanie nie jest prawdą

//|| - operator "lub" - przynajmniej jeden warunek musi być spełniony
let x = 0;
let y = 3;
console.log(x > 3 || y > 2); //true bo drugi warunek jest spełniony

//^ - operator "xor" - przynajmniej jeden warunek musi być spełniony, ale nie wszystkie naraz
let x = 3;
let y = 3;
let z = 5;
console.log(x > 2 ^ y < z); //0 czyli false, bo wszystkie są spełnione

//! - "negacja" czyli odwrócenie true na false i odwrotnie
let x = 2;
let y = 0;
console.log(!true); //false
console.log(!false); //true
console.log(x && y); //false bo y === 0
console.log(!(x && y)) //true

```

### Operatory logiczne w równaniach

```js
// &&
// jeśli pierwsza jest false podstaw drugą wartość
// w przeciwnym wypadku podstaw pierwszą
const a = 100 && 300;
console.log(a); //300 - a jest prawdą, więc weź drugą wartość

const a = 200 && 0;
console.log(a); //0 - a jest prawdą, więc weź drugą wartość

const a = 0;
const b = 200;
const c = a && b;
console.log(c); //0 bo a jest falsy, więc zostań na niej

// ||
// podstawia pod zmienną wartość pierwszą , gdy jest ona inna od falsy
// w przeciwnym wypadku podstaw drugą wartość
const text = 'kot' || 'brak';
console.log(text); //"kot"

const text = '' || 'pies';
console.log(text); //"pies"

const a = 0 || 200;
console.log(a); //200

const a = 200;
const b = 100;
const c = a || b;
console.log(c); //200

const tab = ['ala', 'bala']; //3 elementu nie ma czyli undefined
const x = tab[2] || 'brak';
console.log(x); //"brak"

// ??
// prawa wartość zwracama jest gdy lewa
// ma wartość undefined lub null (nie false)
const x = null || 10;
const y = null ?? 10;
console.log(x); //10
console.log(y); //10

const x = '' || 10;
const y = '' ?? 10;
console.log(x); //10
console.log(y); //""

const tab = ['ala', 'bala'];
const x = tab[2] || 'brak';
const y = tab[2] ?? 'brak';
console.log(x); //"brak"
console.log(y); //"brak"

// w EcmaScript 2021 powyższe możemy bardziej uprościć

// ||=
// podstawi nową wartość tylko wtedy,
// gdy obecna wartość jest false
let a = 0;
let b = 'kot';
a ||= b;
console.log(a); //"kot"

let a = 'pies';
let b = 'kot';
a ||= b;
console.log(a); //"pies"

// &&=
// podstawi pod zmienną nową wartość
// gdy obecna wartość jest inna niż false
let a = 1;
let b = 0;

a &&= 20;
console.log(a); //20

b &&= 20;
console.log(b); //0

// ??=
// podstawi nową wartość, gdy obecna wartość
// jest null lub undefined
let a = null;
a ??= 200;
console.log(a); //200

let a = 0;
a ??= 200;
console.log(a); //0

let a = {
   nr: 100,
};
a.something ??= 200;
a.nr ??= 300;
console.log(a.something); //200
console.log(a.nr); //100
```

# Instrukcje warunkowe

### Wynik sprawdzenia

```js
const a = 10;
const b = 20;

console.log(b > a); //true
console.log(b < a); //false
console.log(b === a); //false

const result = a > b;
console.log(result); //false

const a = 10;
const b = 20;

if (a < b) {
   //kod się wykona
   console.log('A jest mniejsze od B');
}

// W Javascript możemy sprawdzać ze sobą dowolne typy danych.
// ale lepiej konwertować dane do podobnych typów
// przykład poniżej na końcu bloku
const nr = prompt('Podaj jakąś liczbę');
if (nr > 5) {
   console.log(`Liczba ${nr} jest większa od 5`);
}
// powyższe wygląda następująco bo nr to string
if ('7' > 5) {
   console.log(`Liczba 7 jest większa od 5`);
}

// teksty porównywane są litera po literze
console.log('ab' > 'aa'); //true
console.log('pies' > 'kot'); //true
console.log('abc' > 'acc'); //false
console.log('alicja' > 'bela'); //false
console.log('Marcin' > 'Ania'); //true

//  brane są pod uwagę pozycje liter
// na tablicy znaków Unicode
console.log('a' > 'A'); //true
console.log('Kot' > 'kot'); //false
console.log('alicja' > 'Beata'); //true

// inne typy konwertowane są do liczb,
// a następnie porównywane są te liczby
console.log('3' > 2); //true bo 3 > 2
console.log('02' > 3); //false bo 2 > 3
console.log('0' == 0); //true

console.log(true > 2); //false bo true to 1
console.log(false < 2); //true bo false to 0

console.log('Ala' > 0); //false bo konwersja "Ala" na liczbę to NaN (NonANumber), a NaN jest mniejsze od każdej liczby
console.log('Kot' > -Infinity); //false - to samo co powyżej. NaN jest mniejsze od każdej liczby

// najlepiej starać się konwertować dane
// do podobnego typu a nie porównywać jak wyżej
// zamiast
const nr = prompt("Podaj liczbę z zakresu 1-10");
if (nr > 5) { ... }

// lepiej napisać
const nr = Number(prompt("Podaj liczbę z zakresu 1-10"));
if (nr > 5) { ... }
```

### Wartości falsy

```js
// Tworząc warunki, nie musimy porównywać ze sobą dwóch wartości
if (false) { ... }
if (null) { ... }
if (undefined) { ... }
if (0) { ... }
if (NaN) { ... }
if ("") { ... }
if (document.all) { ... }

const a = 20;
const b = 0;
const c = null;

if (a) { //to się wykona bo a !== 0
    console.log("A ma wartość ", a);
}
if (b) { //to się nie wykona bo b === 0
    console.log("A ma wartość ", b);
}
if (c) { //to się nie wykona bo null
    console.log("A ma wartość ", c);
}
if (false) { //to się nie wykona bo false to false
}

// często spotyka się  poniższe

if (nr) { //kod się wykona jeżeli wartość liczby nr jest różna od falsy
}

const txt = "Ala ma kota";
if (txt.length) { //sprawdzam długość tekstu. Jeżeli większa od 0 to true
    ...
}

const tab = []
if (tab.length) { //podobnie sprawdzam długość tablicy
    ...
}
```

### Instrukcja if

```js
// if, wykonuje kod tylko gdy w nawiasach będzie prawda
const nr = Math.random() * 10;

if (nr > 5) {
   console.log('Liczba nr jest większa od 5');
}

// dla każdej instrukcji if możemy zastosować
// zapisy else i else if
const nr = Math.random() * 10;

if (nr >= 5) {
   console.log('Liczba nr jest większa lub równa 5');
} else {
   console.log('Liczba nr jest mniejsza od 5');
}

// lub
const nr = Math.random() * 10;

if (nr < 3) {
   console.log('Liczba jest mniejsza od 3');
} else if (nr <= 6) {
   console.log('Liczba jest mniejsza lub równa 6');
} else {
   console.log('Liczba jest większa od 6');
}
```

### Operator warunkowy

```js
// skrócona wersja warunku if + tzw ternary operator
const x = wyrażenie ? jeżeli_true : jeżeli_false;

// przykład
const i = 1;

let number = '';
if (i > 0) {
   number = 'dodatnia';
} else {
   number = 'ujemna';
}

//to samo tylko w skróconej wersji
const number = i > 0 ? 'dodatnia' : 'ujemna';

// przykłady zastosowania

const x = 23;
const isEven = x % 2 === 0 ? 'parzysta' : 'nieparzysta';
console.log(isEven); //"nieparzysta"

const age = 21;
const status = age < 18 ? 'jesteś za młody' : 'zapraszamy na seans';
console.log(status); //"zapraszamy na seans"

const name = 'Ola';
console.log(name === 'Ola' ? 'Masz na imię Ola' : 'Nie masz na imię Ola'); //"Masz na imię Ola"

const nr = 10;
const answer = nr ? 'yes' : 'no';
console.log(answer);

const isMember = true;
console.log(`Koszt usługi to ${isMember ? '2.00' : '10.00'}zł`);
```

### switch

```js
// instrukcja switch służy do  przyrównywania zmiennej do wartości
const number = prompt('Wpisz jakiego masz zwierzaka');

switch (number) {
   case 'pies':
      console.log('Psy są najlepsze');
      break;
   case 'kot':
      console.log('Koty są lepsze od psów');
      break;
   case 'chomik':
      console.log('Każdy chomik jest super');
      break;
   default:
      console.log('Jakiś dziwny ten zwierzak');
}

// lub
const car = "bmw";

switch (car) {
    case "bmw" : ... break;
    case "fiat" : ... break;
    case "audi" : ... break;
}

```

# Pętle for i while

### Pętla typu for

```js

for (zainicjowanie_zmiennych;  warunek_kończący_wykonywanie_pętli;  zmiana_zmiennych) {
    kod który zostanie wykonany pewną ilość razy
}

// przykłady
for (let i = 0; i < 10; i++) {
   console.log('Wykonanie pętli ', i);
}

// pętla w przeciwnym kierunku
for (let i = 10; i > 0; i--) {
   console.log('Trwa odliczanie', i);
}

// inny warunek kończący
const a = 10;
const b = 20;

for (let i = 1; i <= a && i <= b; i++) {
   //bo oba muszą być prawdziwe
   console.log('Wypisze się tyle co ma mniejsza liczba', i);
}

let a = 10;
let i = 0;
for (; i < 10; ) {
   console.log(i);
   i++;
}
```

### Pętla typu while

```js
while (wyrażenie_sprawdzające_zakończenie_pętli) {
    ...fragment kodu który będzie powtarzany...
}

// przykład
let i = 1;

while (i <= 100) {
    console.log("Nie będę...");
    i++;
}

// while zazwyczaj stosuje się w sytuacjach,
// kiedy nie wiemy dokładnie,
// ile iteracji (powtórzeń) ma się wykonać
let i = 0;

while (i < 0.5) {
    console.log(i);
    i = Math.random();
}

console.log(i);

```

### Pętla typu do while

```js
let i = 0;

do {
   i++;
   console.log(i);
} while (i < 5);

// taki typ pętli wykona się minimum 1 raz
let i = 0;

do {
   i++;
   console.log(i);
} while (false); //warunek od początku nie spełniony ale i tak 1 raz się wykona
```

### Break i continue

```js
// breake kończy dalsze wykonywanie takiej pętli
let str = '';
let i = 0;

while (i <= 100) {
   str += i;
   if (str.length > 20) break;
   i++;
}

console.log(str);

// continue powoduje przerwanie danej iteracji
const tab = ['Ala', 'Monika', 'Beata', 'Karol', 'Alicja'];

for (let i = 0; i < tab.length; i++) {
   if (tab[i] === 'Karol') {
      continue; //Karola pomiń
   }
   console.log(tab[i]);
}

// continue w pętli while, zwiększanie licznika
// musimy robić przed użyciem tej instrukcji.
// Inaczej możemy trafić na moment, gdy aktualne
// powtórzenie będzie przerywane a tym samym
// zwiększanie licznika nigdy nie nastąpi
let i = 0;
let sum = 0;

while (i < 5) {
   i++;
   if (i === 3) continue;
   sum += i;
   console.log(i, `suma kolejnych liczb to ${sum}`);
}
```

### Labele dla pętli

```js
// Dzięki nim możemy stosować instrukcje
// break i continue dla pętli o danej nazwie

// break
first: for (let i = 0; i < 10; i++) {
   second: for (let j = 0; j < 10; j++) {
      if (warunek) break first; //przerywam główną pętlę
   }
}

// continue
loopA: for (let i = 0; i < 10; i++) {
   loopB: for (let j = 0; j < 10; j++) {
      if (warunek) continue loopA;
   }
}
```

# Number i Math

```js
// Number - czyli typ danychh
// pozwalający pracować na liczbach
const nr1 = 102;
const nr2 = 1.25;

const nr1 = 1e6; //1 * 1000000
const nr2 = 2e5; //2 * 100000
const nr3 = 1.3e4; //1.3 * 10000

const nr1 = 1e-5; //5 zer na lewo od liczby => 0.00001
const nr2 = 2e-3; //3 zera na lewo 0.002
const nr3 = 2.1e-4; //4 zera na lewo 0.00021

// zapis liczb systemm dwójkowym,
// hexadecymalnym oraz ósemkowym

//szesnastkowy
console.log(0xff); //255
console.log(0x66); //102

//ósemkowy
const nr1 = 0o377; //255

//dwójkowy
const nr2 = 0b11111111; //255
```

### Funkcja toString()

```js
const nr = 150;
console.log(nr.toString(16)); //"96"
console.log(nr.toString(10)); //"150"
console.log(nr.toString(2)); //"10010110"
console.log(nr.toString()); //"150" - domyślnie dziesiętny
```

### Math

```js
const var1 = 56.5;
const var2 = 74.3;

Math.min(var1, var2); //56.5
Math.max(var1, var2); //74.3
Math.max(1, 3, 6, 2); //6

// wartość bezwzględna
Math.abs(-1); //1

// zwraca daną liczbę zaokrągloną
// do najbliższej liczby całkowitej
Math.round(var1); //57
Math.round(20.52); //21
Math.round(-10.21); //-10
Math.round(-11.82); //-12

// zwraca największą liczbę całkowitą
// mniejszą od lub równą danej
Math.floor(var1); //56
Math.floor(20.52); //20
Math.floor(-10.21); //-11
Math.floor(-11.82); //-12

// zwraca najmniejszą liczbę całkowitą
// większą od lub równą danej
Math.ceil(var1); //57
Math.ceil(20.52); //21
Math.ceil(-10.21); //-10
Math.ceil(-11.82); //-11`

// sprawdza czy argument jest dodatni, ujemny czy zerem.
Math.sign(5); // 1
Math.sign(-5); // -1
Math.sign(0); // 0
Math.sign('text'); // NaN

// zwraca pierwiastek kwadratowy danej liczby.
Math.sqrt(4); // 2

//zwraca daną liczbę podniesioną do danej potęgi
// Math.pow(podstawa, wykładnik)
Math.pow(2, 3); // 8

//zwraca liczbą pseudolosową z przedziału 0 do 1
Math.random(); // np 0.23489431423129448
```

### Losowa liczba z przedziału

```js
const min = 3;
const max = 7;

const result = Math.floor(Math.random() * (max - min + 1) + min);
```

# Stringi

```js
const text = 'Ala ma kota, a kot ma Ale.'; //""podwójne cudzysłowy zwykłe "
const text = 'Ala ma kota'; //pojedyncze apostrofy
const img = '<div class="element" data-text="test">';
const txt = "It's a big year";
const text = `Ala ma kota`; // backtiki też są prawidłowe
```

### Teksty na wiele linii

```js
//poprzez operator przypisania
let text = 'Stoi na stacji lokomotywa,';
text += 'Ciężka, ogromna i pot z niej spływa:';
text += 'Tłusta oliwa.';

//poprzez dodawanie części tekstu
let text =
   'Stoi na stacji lokomotywa,' +
   'Ciężka, ogromna i pot z niej spływa:' +
   'Tłusta oliwa.';

//Poprzez zastosowanie znaku backslash na końcu linii
let text =
   'Stoi na stacji lokomotywa,\
Ciężka, ogromna i pot z niej spływa:\
Tłusta oliwa.\
';

//Najlepsza metoda - użycie template strings
let text = `Stoi na stacji lokomotywa,
Ciężka, ogromna i pot z niej spływa:
Tłusta oliwa.`;
```

### Wstawianie zmiennych do tekstu

```js
const age = 10;
const text = 'Ten pies ma ' + age + ' lat'; // "" tu wszystkie są zwykłe "
const text = 'Ten kot ma ' + age + ' lat';
const text = `Ten chomik ma ${age} lat`; // nie wszystkie przeglądarki obsługują
```

### Pobieranie długości tekstu

```js
const text = 'Ala';
text.length; //3
'Koty i psy są fajne'.length; //19
```

### Pobieranie znaku na danej pozycji

```js
const text = 'Ala ma kota, a kot ma Ale';

console.log(text.charAt(0)); //A
console.log(text.charAt(4)); //m

console.log(text[0]); //A
console.log(text[4]); //m
```

### toUpperCase() i toLowerCase() - zamiana wielkości liter

```js
const text = 'Ala ma kota';

console.log(text.toUpperCase()); //"ALA MA KOTA"
console.log(text.toLowerCase()); //"ala ma kota"
```

### indexOf() i lastIndexOf() - zwracanie pozycji szukanego tekstu

```js
// powyższe metody dostępne są dla stringów i tablic
const text = 'Ala ma kota';
console.log(text.indexOf('m')); // 4 - zwraca pozycję pierwszego napotkanego m

const text = 'Ala ma kota';
console.log(text.indexOf('f')); // -1 bo nie ma w stringu f

const text = 'Ala ma kota';
console.log(text.indexOf('kota')); // 7

const text = 'Ala ma kota';
console.log(text.lastIndexOf('a')); // 10 - zwraca ostatnią pozycję na której jest a
```

### startsWith() i endsWith() - czy zaczyna się i kończy

```js
// zwraca true lub false jeśli string
// zaczyna się lub kończy na podaną wartość
const text = 'Ala ma kota';

text.startsWith('Ala'); //true
text.startsWith('Ola'); //false

text.endsWith('kota'); //true
text.endsWith('psa'); //false
```

### substr() - zwracanie kawałka tekstu

```js
// zwraca kawałek tekstu substr(start, dlugosc)
const text = 'Ala ma kota';

console.log(text.substr(2)); // "a ma kota"
console.log(text.substr(0, 3)); // "Ala"
console.log(text.substr(7, 4)); // "kota"
console.log(text.substr(4)); // "ma kota"
```

### substring() - zwracanie kawałka tekstu

```js
// zwraca akawałek tekstu substring(start, stop)
// działa podobnie jak powyższa ale drugi
// parmetr wskazuje miejsce końca pobierania
const text = 'Ala ma kota';

console.log(text.substring(0, 3)); //"Ala"
console.log(text.substring(3)); //"ma kota"
console.log('Ala ma kota'.substring(6, 4)); //"ma" 6 i 4 zostają automatycznie zamienione miejscami
```

### `slice`() - zwracanie kawałka tekstu

```js
// metoda dostępna dla stringow i tablic
// działa identycznie jak substring() ale nie zamienia
// argumentów miejscami jeśli drugi jest mniejszy
const txt = 'Ala ma kota';

const txt2 = txt.slice(0, 3);
console.log(txt2); // "Ala"

const txt3 = txt.slice(1, 5);
console.log(txt3); // "la m"

const txt4 = txt.slice(4, 6);
console.log(txt4); // "ma"

const txt5 = txt.slice(4);
console.log(txt5); // "ma kota"

const txt6 = txt.slice(-4);
console.log(txt6); // "kota"
```

### split() - dzielenie tekstu

```js
// split(znak, dlugosc) zwraca tablicę
// z podzielonych fragmentów tekstu
// znak = znak podziału stringa, dlugosc = ilosc elemntow tablicy
const text = 'Ala ma kota, a kot ma Alę, Ala go kocha';
const parts = text.split(', ');
console.log(parts); // (3) ["Ala ma kota","a kot ma Alę","Ala go kocha"]

const text = 'Ala ma kota, a kot ma Alę, Ala go kocha';
const parts = text.split(', ', 1);
console.log(parts); // (1) ["Ala ma kota"]
```

### replace() - wyszukiwanie tekstu i jego zamiana

```js
// metoda replace(ciag_szukany, zamieniony)
// zwraca nowy tekst, w którym został zamieniony
// szukany ciąg znaków na nowy tekst.
const text = 'Ala ma kota';
const textNew = text.replace('kota', 'psa');
console.log(textNew); //"Ala ma psa"

// wyszukuje i zamienia tylko pierwsze wystąpienie
const text = 'Ola lubi koty, Ola lubi psy';
const textNew = text.replace('Ola', 'Ela');
console.log(textNew); //"Ela lubi koty, Ola lubi psy"

// Aby zostały zamienione wszystkie wystąpienia
//szukanego ciągu, musimy zastosować
// wyrażenie regularne.
const text = 'Ola lubi koty, Ola lubi psy';
const textNew = text.replace(/Ola/g, 'Ela'); //g jak globalnie w całym tekście
console.log(textNew); //"Ela lubi koty, Ela lubi psy"
```

### repeat() - powtarzanie tekstu

```js
const text = 'kot';
console.log(text.repeat(3)); //kotkotkot
'u'.repeat(10); // uuuuuuuuuu
```

### Pętla po tekście

```js
const txt = 'abecadło';

for (let i = 0; i < txt.length; i++) {
   console.log(txt[i]);
}

for (const el of txt) {
   console.log(el);
}
```

# Array

```js
//Array:
let owoce = ['Jabłko', 'Banan']; // lub jak poniżej
let owoce = new Array('Jabłko', 'Banan');

console.log(owoce.length); // 2
let pierwszy = owoce[0]; // Jablko

owoce.forEach(function (item, index, array) {
   console.log(item, index);
});
// Jablko 0
// Banan 1

let a = owoce.push('Pomarańcz'); // ['Jabłko', 'Banan', 'Pomarańcz'], a=3 - ile elementów jest w tablicy
let b = owoce.pop(); // usuwa pomarańczę z końca // ['Jabłko', 'Banan']; b=Pomarańcz
let c = owoce.shift(); // usuwa jabłko z początku // ['Banan'], c=Jabłko
let d = owoce.unshift('Truskawki'); // dodaje na początku // ['Truskawki','Banan'], d=2 - ile elementów jest w tablicy
let pos = owoce.indexOf('Banan'); // pos=1, zwraca indeks elementu tablicy

// Array.isArray()
const tab = ['ala', 'bala'];
const ob = { name: 'Piotr' };

console.log(Array.isArray(tab)); //true
console.log(Array.isArray(ob)); //false

console.log(typeof tab); //"object";
console.log(typeof ob); //"object";
```

### join() - scalanie tablicy w tekst

```js
onst ourTable = ["Marcin", "Ania", "Agnieszka"];
console.log(ourTable.join()); //wypisze się "Marcin,Ania,Agnieszka"
console.log(ourTable.join(" - ")); //wypisze się "Marcin - Ania - Agnieszka"
console.log(ourTable.join(" <--> ")); //wypisze się "Marcin <--> Ania <--> Agnieszka"
```

### Zamiana tekstu na tablicę

```js
const txt = 'kartofel';
const tab = [...txt];
console.log(tab); //["k", "a", "r", "t", "o", "f", "e", "l"]

const txt = 'Ala ma kota';
const tab = txt.split(' ');
console.log(tab); //["Ala", "ma", "kota"];
```

### reverse() - odwracanie kolejności elementów tablicy

```js
const tab = [1, 2, 3, 4];

console.log('Przed: ' + tab); //Przed: [1, 2, 3, 4]
tab.reverse();
console.log('Po: ' + tab); //Po: [4, 3, 2, 1]

const word = 'kajak';
const tab = [...word];
console.log(tab.reverse().join('') === tab.join('')); //true czyli palindrom
```

### indexOf(), lastIndexOf() i includes() wyszukiwanie elementu w tablicy

```js
// indexOf() Zwraca index szukanego tekstu lub -1 jeśli nie znajdzie
const tab = ['Marcin', 'Ania', 'Agnieszka', 'Monika'];
let a = tab.indexOf('Agnieszka'); // a=2
let b = tab.indexOf('Genowefa'); // a=-1

// lastIndexOf() zwraca ostatnią pozycję szukanego tekstu
const tab = ['Agnieszka', 'Marcin', 'Ania', 'Agnieszka', 'Monika'];
const index = tab.lastIndexOf('Agnieszka'); // index=3

// includes() zwraca prawdę lub fałsz
//w zależności czy szukana wartość znajduje się w tablicy

const tab = ['Marcin', 'Ania', 'Agnieszka', 'Monika'];
let a = tab.includes('Ania'); // true
let b = tab.includes('Henryk'); // false
```

### splice() - usuwanie lub dodawanie elementów

```js
// służy zarówno do usuwania jak i wstawiania
//nowych elementów do tablicy.
const tab = ['Marcin', 'Ania', 'Agnieszka', 'Monika'];
tab.splice(2, 1); //usuwam 1 element na indeksie 2
console.log(tab); //["Marcin", "Ania", "Monika"]

const tab = ['Marcin', 'Ania', 'Agnieszka', 'Monika'];
tab.splice(1, 0, 'A', 'B'); //nic nie usuwam i wstawiam nowe elementy przed indeks 1
console.log(tab); //["Marcin", "A", "B", "Ania", "Agnieszka", "Monika"]
```

### fill() - wypełnianie tablicy

```js
const tab = new Array(20);
console.log(tab); //[empty x 20]
tab.fill('kot');
console.log(tab); //["kot", "kot", "kot", ...]

const tab2 = [];
tab2.length = 15;
console.log(tab2); //[empty x 15]
tab2.fill('kot', 2, 5);
console.log(tab2); //[empty × 2, "kot", "kot", "kot", empty × 10]

const tab3 = [1, 2, 3, 4, 5];
tab3.fill('pies', 2);
console.log(tab3); //[1, 2, "pies", "pies", "pies"]
```

### concat() - łączenie tablic

```js
// nie możemy używać zwykłego dodawania bo
// zadziała automatyczna konwersja typów czyli toString();
const tab1 = ['Ala', 'Basia'];
const tab2 = ['Piotr', 'Marcin'];
console.log(tab1 + tab2); //Ala,BasiaPiotr,Marcin

const anim1 = ['Pies', 'Kot'];
const anim2 = ['Słoń', 'Wieloryb'];
const anim3 = ['Chomik', 'Świnka'];
const table = anim1.concat(anim2);
console.log(table); //wypisze ["Pies", "Kot", "Słoń", "Wieloryb"]
const tableBig = anim1.concat(anim2, anim3);
console.log(tableBig); //wypisze ["Pies", "Kot", "Słoń", "Wieloryb", "Chomik", "Świnka"];
```

### slice() - zwracanie kawałka tablicy

```js
const tab = ['Marcin', 'Ania', 'Agnieszka', 'Monika', 'Magda'];

const tab2 = tab.slice(0, 1);
console.log(tab2); //["Marcin"]
console.log(tab); //["Marcin", "Ania", "Agnieszka", "Monika", "Magda"]

const tab3 = tab.slice(2);
console.log(tab3); //["Agnieszka", "Monika", "Magda"]

const tab5 = tab.slice(-2); //od końca
console.log(tab5); //["Monika", "Magda"]

const tab6 = tab.slice(2, -1);
console.log(tab6); //["Agnieszka", "Monika"]
```

### Pętle po tablicy

```js
const tab = ['Marcin', 'Ania', 'Agnieszka'];

// pętla for
for (let i = 0; i < tab.length; i++) {
   console.log(tab[i]); //"Marcin", "Ania"...
}
// pętla for of
for (const el of tab) {
   //el to nazwa zmiennej wymyślona przez nas
   console.log(el); //"Marcin", "Ania", "Agnieszka"
}
```

### Tablice wielowymiarowe

```js
const tab = [
   ['a1', 'a2', 'a3', 'a4', 'a5', 'a6'],
   ['b1', 'b2', 'b3', 'b4', 'b5', 'b6'],
   ['c1', 'c2', 'c3', 'c4', 'c5', 'c6'],
];
```

### flat() - spłaszczanie tablicy wielowymiarowej

```js
const tab = [
   1,
   [2, 3],
   [4, 5, [6, 7]],
   [
      [
         [8, 9],
         [10, 11],
      ],
   ],
];

console.log(tab.flat(2));
```

### Array.from()

```js
// Array.from(ob, map*, this*)
// służy do tworzenia tablic z obiektów tablico podobnych
const ob = {
   0: 'ala',
   1: 'bela',
   length: 2,
};
console.log(Array.from(ob)); //["ala", "bela"]

//pobieram kolekcję buttonów ze strony
const buttons = document.querySelectorAll('button');
console.log(buttons); //NodeList [button, button...]
const tab = Array.from(buttons);
console.log(tab); //Array [button, button...]

//Drugi opcjonalny parametr tej funkcji może
//zawierać funkcję map() dla tablic:
const ob = {
   0: 'ala',
   1: 'bela',
   length: 2,
};

const tab = Array.from(ob, function (el) {
   return el.toUpperCase();
});
console.log(tab); //["ALA", "BELA"]
```

### sort() - sortowanie tablicy

```js
const tab = ['Marcin', 'Ania', 'Piotrek', 'Grześ'];
tab.sort();
console.log(tab); //wypisze się "Ania, Grześ, Marcin, Piotrek"

const tab = [1, 2, 21, 2.1, 32, 3.1]; // sort() traktuje liczby jak litery
tab.sort();
console.log(tab); //[ 1, 2, 2.1, 21, 3.1, 32 ]

const tab = ['Bartek', 'ania', 'Celina', 'agnieszka']; // źle bo duże litery są przed małymi
tab.sort();
console.log(tab); //["Bartek", "Celina", "agnieszka", "ania"]

// żeby uniknąć powyższego błędu musimy do funkcji sort()
// przekazać własną funkcję sortującą
function mySort(a, b) {
   //..
}
tab.sort(mySort);

// Ogólna postać funkcji sortującej wygląda tak: (BubleSort)
const tab = ['Marcin', 'Ania', 'Agnieszka'];
function compare(a, b) {
   if (a < b) {
      return -1;
   }
   if (a > b) {
      return 1;
   }
   return 0;
}
tab.sort(compare);
console.log(tab);

// do wartości liczbowych musimy utworzyć funkcję
// ----- DO SPRAWDZENIA BO POWYŻSZA CHYBA TEŻ SORTUJE LICZBY -----
function compareNr(a, b) {
   return a - b;
}
const tab = [100, 320, 10, 25, 310, 1200, 400];
const tab3 = tab.sort(compareNr);
console.log(tab3); //[10, 25, 100, 310, 320, 400, 1200]

// inny przykład funkcji sortującej
const tab = [
   { name: 'Marcin', height: 183 },
   { name: 'Ania', height: 173 },
   { name: 'Agnieszka', height: 170 },
];
//dla sort spokojnie możemy używać funkcji anonimowej
tab.sort(function (a, b) {
   return a.height - b.height;
});
for (let a of tab) {
   console.log(a);
}

// jeszcze inny przykład funkcji sortującej
// porównanie stringów
const tab = [
   { name: 'Marcin', height: 183 },
   { name: 'Ania', height: 173 },
   { name: 'Agnieszka', height: 170 },
];
tab.sort(function (a, b) {
   //tekstów nie możemy odejmować. Możemy je porównywać poprzez > <, ale nie odejmować
   return a.name.localeCompare(b.name);
});
for (let elem of tab) {
   console.log(elem);
}

// przykład sortowania złożonej tablicy
const users = [
   {
      name: 'Marcin',
      car: {
         name: 'Toyota',
         age: 10,
      },
   },
   {
      name: 'Marcin',
      car: {
         name: 'Fiat',
         age: 15,
      },
   },
   {
      name: 'Monika',
      car: {
         name: 'BMW',
         age: 5,
      },
   },
];
//sortuje po wieku samochodu
users.sort((a, b) => {
   return a.car.age - b.car.age;
});
console.log(users);
```

# Funkcje

```js
// podstawowa deklaracja funkcji
function nazwaFunkcji(nr) {
   const result = nr * nr;
   return result;
}

// wywołanie
nazwaFunkcji(2); //4
nazwaFunkcji(3); //9
nazwaFunkcji(5); //25
nazwaFunkcji(); //NaN

// Jeżeli nasza funkcja wymaga pewnych
// wartości, a my ich nie podamy, zostaną
// użyte dla nich wartości undefined
function writeText(name, age) {
   console.log(`${name} ma kota, który ma ${age} lat`);
}

writeText('Ala', 5); //"Ala ma kota, który ma 5 lat"
writeText('Marysia'); //"Marysia ma kota, który ma undefined lat"
writeText(); //"undefined ma kota, który ma undefined lat"
```

### Domyślne wartości funkcji

```js
// Wystarczy po nazwie parametru
// ustawić mu domyślną wartość
function print(name = 'Michał', status = 'najlepszy') {
   console.log(name + ' jest ' + status);
}

print(); //"Michał jest najlepszy"
print('Karol'); //"Karol jest najlepszy"
print('Paweł', 'wysoki'); //"Paweł jest wysoki"
print(undefined, 'wysoki'); //"Michał jest wysoki" - undefined jest traktowane jak niepodanie wartości
```

### arguments i rest

```js
// Jeżeli nie zakładamy konkretnej liczby parametrów
// możemy skorzystać z właściwości arguments,
// która zawiera w sobie wszystkie przekazane wartości:

function show() {
   console.log(arguments);
}

show(); // []
show(1, 2, 3, 4); // [1, 2, 3, 4]
show('ala', 'ma', 'kota'); // ["ala", "ma", "kota"]

// Obiekt arguments jest tablico podobny,
// ale tak naprawdę nie jest tablicą.
// Oznacza to, że nie możemy na nim wykonywać
// metod przeznaczonych dla tablic np. reduce, map i podobnych:

// rest operator, zbiera przekazane
// argumenty w postaci klasycznej tablicy

function myF(...param) {
   console.log(param);
}

myF(1, 2, 3, 4, 5); // [1, 2, 3, 4, 5]

// inny przykład
function myF(...param) {
   const newTab = [...param];
   newTab.push('Ala');
   console.log(param, newTab);
}

myF(1, 2, 3); // [1,2,3], [1,2,3,"Ala"]

// Rest operator możemy też wykorzystywać d
// o pobierania w formie tablicy
// "pozostałych" wartości:
function printAbout(name = 'Ala', ...other) {
   console.log('To jest ' + name);

   if (other.length) {
      console.log(`${name} ma zwierzaki: ${other}`);
   }
}

printAbout('Marcin', 'pies', 'kot'); //To jest Marcin. Marcin ma zwierzaki: pies,kot
printAbout(); //To jest Ala

// WAŻNE: rest musi występować jako
// ostatni w parametrach:
function myF(a, b, ...numbers) {
}

function myF(a, ...numbers, b) { // błąd
}
```

### Instrukcja return

```js
function calculate(number1, number2) {
   const result = number1 + number2;
   return result;
}

calculate(10, 4); //wypisze 14

// return przerywa dalsze działanie funkcji
function sum(a, b) {
   return a + b;

   console.log(a + b); //nigdy nie zostanie wykonane,
   console.log('Test');
}

// instrukcji return może być wiele dla
// jednej funkcji. Zawsze jednak wykonana
// zostanie tylko jedna
function getStatus(number) {
   if (number < 20) {
      return 'bad';
   }

   if (number < 30) {
      return 'medium';
   }

   return 'good';
}
console.log(getStatus(10));
console.log(getStatus(25));

// instrukcja return może zwracać dowolną wartość
// np tablicę
function returnArray() {
   return [4, 3, 5, 8];
}
let a = returnArray();
console.log(a[0]); //4

// np obiekt
function returnObject() {
   return {
      first: 'ala',
      second: 'bala',
      third: 'cala',
   };
}
console.log(returnObject().first); //"ala"
```

### Wyrażenia funkcyjne

```js
// czyli podstawienie funkcji pod zmienną
const printText = function () {
   console.log('ala ma kota');
};
printText();

// hoisting nie działa w przypadku
// wyrażenia funkcyjnego
myFunction(); //Błąd

const myFunction = function () {
   console.log('...');
};

// przy zwykłej deklaracji funkcji działa
myFunction(); //Tutaj jest ok

function myFunction() {
   console.log('...');
}

// inna różnica między deklaracją
// w klasyczny sposób i wyrażeniem funkcyjnym
function testX() {
   console.log('x');
}

const textY = function () {
   console.log('y');
};

window.testX(); //"x"
window.testY(); //błąd
```

### Funkcja anonimowa

```js
// funkcja anonimowa to taka funkcja,
// która nie ma swojej nazwy
// wykorzystywane są jako funkcje zwrotne,
// które przekazujemy do innych funkcji
document.addEventListener('click', function () {
   console.log('klik');
});

[1, 2, 3].forEach(function (el) {
   console.log(el);
});

[1, 2, 3].sort(function (a, b) {
   return a - b;
});
```

# Funkcja strzałkowa

```js
// funkcja strzałkowa to skrócony
// zapis wyrażenia funkcyjnego
const myFn = function () {};

// to co powyżej można zapisać:
const myFn = () => {};

// przy jednym argumencie można pominąć nawiasy
const myF = function (a) {
   console.log(a * a);
};

// to co powyżej  można zapisać: (a) lub a
const myF = (a) => {
   console.log(a * a);
};

// jeżeli parametrów jest więcej,
// lub nie ma żadnego, wtedy nawiasy muszą zostać:
const myF = function () {
   console.log('Ala ma kota');
};

const myF = () => {
   console.log('Ala ma kota');
};

// jeżeli funkcja ma tylko jedną
// instrukcję, można pominąć też klamry
const myF = function (a) {
   console.log(a * a);
};

const myF = (a) => console.log(a * a);

//  jeżeli jedyną instrukcją jest
// instrukcja return, także i jej można się pozbyć
const myF = function (a) {
   return 'Wynik to: ' + a * a;
};

const myF = (a) => 'Wynik to: ' + a * a;

//  jeżeli funkcja ma więcej instrukcji
// klamry muszą pozostać
const myF = function (a, b) {
   const result = a * b;
   console.log('Wynik mnożenia to', result);
   return result;
};

const myF = (a, b) => {
   const result = a * b;
   console.log('Wynik mnożenia to', result);
   return result;
};

// jeżeli jedyną instrukcją jest zwracanie obiektu,
// zachodzi konflikt między redukcją klamer, a klamrami obiektu.
// zwracany obiekt trzeba objąć nawiasami
const getObj = function(name) {
    return { team : name, score : 0 }
}

const getObj = name => { team : name, score : 0 } //błąd
const getObj = name => ({ team : name, score : 0 }) //ok

// INFO
// 1.
// Funkcje strzałkowe nie mają wiązania this i super.
// Dlatego nie powinniśmy ich używać do definiowania
// metod w obiektach i klasach

// 2.
// Nie posiadają właściwości arguments i new.target

// 3.
// Użycie dla nich call, apply i bind
// nie da oczekiwanych rezultatów ( bo nie ma powiązania this)

// 4.
// Nie można ich używać jako konstruktorów

// 5.
// Nie wolno używać w nich yield


```

# Spread

### Spread

```js
// umożliwia rozbijanie iterowanej
// wartości na składowe
// stringów, tablic, obiektów, kolekcji
//rozbijanie tablicy na poszczególne liczby
const tab = [1, 2, 3, 4];
console.log(...tab); //1, 2, 3, 4

//kopiowanie tablicy
const tab2 = [...tab];

//łączenie tablic
const tabPart = [3, 4];
const tabFull = [1, 2, ...tabPart, 5, 6]; //[1, 2, 3, 4, 5, 6]

//rozdzielanie tekstu na poszczególne litery
const str = 'Ala';
const tab = [...str]; //["A", "l", "a"]

// Math.max wymaga parametrów po przecinku
// nie jako tablica więc można tutaj zastosować spread:

const tab = [1, 2, 3, 5, 4];
Math.max(...tab); //5

// spread wykorzystuje się do zamiany kolekcji
// elementów na tablicę, dzięki czemu można
// używać dla nich metod tablicowych

const divs = document.querySelectorAll('div');
//nowa tablica z samymi tekstami z divów
const texts = [...divs].map((el) => el.innerText);

// spread możemy też zastosować dla obiektów

const ob1 = {
   a: 10,
   b: 20,
};

const ob2 = {
   a: 15,
   c: 30,
};

const obBig = {
   ...ob1,
   ...ob2,
   d: 40,
};

console.log(obBig); //{ a : 15, b : 20, c : 30, d : 40 }
```

# Obiekty

### Tworzenie pojedynczego obiektu

```js
const dog = {
   name: 'Szama',
   speed: 1000,
   showText: function () {
      return 'To jest pies';
   },
};

// metody dla obiektów można definiować
// bez słowa function
// zamiast powyższego  można:
const dog = {
   name: 'Szama',
   speed: 1000,
   showText() {
      return 'To jest pies';
   },
};

// jeżeli pod klucze podstawiamy
// wartości z jakiś zmiennych i mają
// te same nazwy  to możemy:
const name = 'Szama';
const speed = 1000;

// zamiast
const dog = {
   name: name,
   speed: speed,
   showText() {
      return 'To jest pies';
   },
};

// możemy napisać
const dog = {
   name,
   speed,
   showText() {
      return 'To jest pies';
   },
};

// niby skromne, a ma sporą moc
const tab = [];
const name = 'Szama';
const speed = 1000;

//zamiast
const ob = {
   name: name,
   speed: speed,
};
tab.push(ob);

//mogę
tab.push({
   name: name,
   speed: speed,
});

//lub jeszcze lepiej
tab.push({ name, speed });
```

### Odwoływanie się do właściwości

```js
// Do właściwości i metod obiektu
// możemy się odwoływać na dwa sposoby
const dog = {
   name: 'Szama',
   speed: 1000,
   showText() {
      return 'Jestem psem';
   },
};
// 1
//poprzez kropkę po której podajemy nazwę klucza
dog.name; //"Szama"
dog.speed; //1000
dog.showText(); //"Jestem psem"

// 2
//używając kwadratowych nawiasów
dog['name']; //"Szama"
dog['speed']; //1000
dog['showText'](); //"Jestem psem"

// czasami kwadratowe nawiasy
// są niezbędne
const calendar = {
    "2021-11-11" : "Narodowe Święto Niepodległości"
}
calendar.2021-11-11 //oczywisty błąd bo odejmujemy od 2021 resztę liczb
calendar["2021-11-11"] //"Narodowe Święto Niepodległości"

// zamist powyższych dwóch metod
// można użyć tzw. przypisania destrukturyzacji
const obj = {
    name: "Marcin",
    surname: "Kowalski",
    age: 10
}

//zamiast
const name = obj.name;
const surname = obj["surname"];
const age = obj.age;

//mogę
const {name, surname, age} = obj;

// to samo w tablicach, które
// także są obiekatami
// dokładny opis w destrukturyzacji obiektów
const tab = ["Ala", "Ola", "Ela"];

//zamiast
const name1 = tab[0];
const name2 = tab[1];

//mogę
const [name1, name2] = tab;
```

### Dodawanie nowych właściwości

```js
// możemy dodawać metody i właściwości
// w ciele obiektu ale także poza nim
const dog = {
   name: 'Szama',
   speed: 1000,
   showText() {
      return 'Jestem psem';
   },
};

dog.type = 'pies';
dog.legs = 4;
dog.eat = function () {
   return 'Jem dobre rzeczy';
};

dog.eat();
dog.showText();

// do zapisu kluczy wewnątrz obiektu można
// też użyć notacji z kwadratowymi nawiasami
// we wcześniejszych wersjach trzeba było
// to robić poza obiektem
// Przydaje się raczej przy bardziej
// zaawansowanym programowaniu,
// gdzie używa się Symboli.

//ES5
const obj = {
    name: "Karol",
    surname: "Nowak"
}
obj["my pet"] = "Pies";
obj["eat food"] = function() {
    return "Lubię jeść jabłka";
}

//ES6
const obj = {
    name: "Karol",
    surname: "Nowak"
    ["my pet"] : "Pies",
    ["eat food"]() {
        return "Lubię jeść jabłka";
    }
}

obj["my pet"] //"Pies"
obj["eat food"]() //"Lubię jeść jabłka"


```

### Obiekty w obiektach

```js
const person = {
   name: 'Marcin',

   pet: {
      name: 'Szama',
      color: 'brown',
      speed: 1000,

      collar: {
         color: 'red',
         length: '25cm',
      },

      favoriteFood: ['mięso', 'mięso', 'mięso'],
   },
};

person.name; //"Marcin"
person.pet.name; //"Szama"
person.pet.collar.color; //"red"
person.pet.favoriteFood[1]; //"mięso"
```

### this

```js
const car = {
   brand: 'Mercedes',
   color: 'czerwony',
   showText() {
      console.log(`${this.brand} koloru ${this.color}`);
   },
};

car.drive = function () {
   console.log(this.brand + ' - jadę!');
};

car.showText(); //"Mercedes koloru czerwony"
car.drive(); //"Mercedes - jadę!"

// dzięki temu możemy np użyć
// pojedyńczej funkcji dla kilku obiektów
function show() {
   console.log(`${this.brand} koloru ${this.color}`);
}

const car1 = {
   brand: 'Mercedes',
   color: 'czerwony',
   showText: show,
};

const car2 = {
   brand: 'BMW',
   color: 'czarny',
   showText: show,
};

car1.showText(); //"Mercedes koloru czerwony"
car2.showText(); //"BMW koloru czarny"

// global context

// Jeżeli nasz kod uruchamiany jest
// z najwyższego poziomu to wskauje na window
// dla środowiska Node.js jest to Object [global]
console.log(this); // window

// w każdym momencie możemy odwołać się
// do tego globalnego kontekstu
// poprzez użycie zmiennej globalThis
const ob = {
   show() {
      console.log(this); //ob
      console.log(globalThis); //window
      console.log(globalThis === window); //true
   },
};

ob.show();

// function context

// jeśli funkcja nie jest metodą obiektu
// to this będzie wskazywało na obiekt globalny
console.log(this); //window

function test() {
   console.log(this); //window
}

test();

// wyjątkiem jest używanie strict mode
// lub używanie modułów ES6 które automatycznie
// włączają strict mode
// "use strict;"
('use strict;');

console.log(this); //window dla przeglądarki lub module.exports dla Node.js

function test() {
   console.log(this); //undefined
}

test();

// jeśli funkcja jets metodą obiektu
// to this wskazuje na ten obiekt
const ob = {
   name: 'pies',
   show() {
      console.log(this); //ob
   },
};

ob.show();

// tak samo dzieje sie w innych obiektach
Math.max(...) //this w metodzie max() wskazuje na Math
[1,2,3,4].push(5) //this w metodzie push() wskazuje na tablicę
window.alert() //this w metodzie alert() wskazuje na window
"Ala ma kota".toUpperCase() //this w metodzie toUpperCase() wskazuje na tekst

// powyższe zasady tyczą się każdego
// poziomu zagnieżdżenia
function testX() {
    console.log(this); //window
}
testX();

const ob = {
   name : "pies",

   show() {
        console.log(this); //ob

        //poniższa funkcja NIE JEST metodą obiektu ob
        //ani metodą poniższego obiektu obj
        function testY() {
            console.log(this); //window
        }
        testY();

        const obj = {
            show() {
                console.log(this); //obj
            }
        }
        obj.show();
   }
}

ob.show();

// zmiana kontekstu this
// bind() i funkcja strzałkowa
const ob = {
    pets : ["kot", "pies", "chomik"],

    bindButton() {
        console.log(this); //ob
        console.log(this.pets); //["kot", "pies", "chomik"]

        //pobieramy przycisk
        const btn = document.querySelector("button");

        //podpinamy mu nasłuchiwanie kliknięcia
        btn.addEventListener("click", function() {
            console.log(this); //button

            //?????? - jak się odwołać do powyższej tablicy pets?
            //skoro this wskazuje na buttona
            console.log(this.pets);
        });
    }
}

ob.bindButton();

// 1. funkcja bind(newThis, param1*, param2*...)
const ob = {
    pets : ["kot", "pies", "chomik"],

    bindButton() {
        const btn = document.querySelector("button");
        btn.addEventListener("click", function() {
            console.log(this.pets);
        }.bind(this));
    }
}

ob.bindButton(); //["kot", "pies", "chomik"],

//
const ob = {
    pets : ["kot", "pies", "chomik"],

    showPets() {
        console.log(this.pets);
    },

    bindButton() {
        const btn = document.querySelector("button");
        btn.addEventListener("click", this.showPets.bind(this));
    }
}

ob.bindButton();

// 2. lub funkcja strzałkowa
const ob = {
    pets : ["kot", "pies", "chomik"],

    showPets() {
        console.log(this.pets);
    },

    bindButton() {
        const btn = document.querySelector("button");

        btn.addEventListener("click", function() {
            this.showPets(); //błąd bo btn nie ma takiej metody
        });

        btn.addEventListener("click", () => {
            this.showPets(); //["kot", "pies", "chomik"]
        });

        //lub krócej
        btn.addEventListener("click", () => this.showPets());
    }
}

ob.bindButton();

// 3. bind() wraz z funkcją strzałkową
// stosowana w klasowych komponentach Reacta
const ob = {
    pets : ["kot", "pies", "chomik"],

    showPets() {
        console.log(this.pets);
    },

    bindButton() {
        this.showPets = this.showPets.bind(this);

        const btn = document.querySelector("button");
        btn.addEventListener("click", this.showPets);
    }
}

ob.bindButton();


```

### Usuwanie właściwości i metod

```js
// aby usunąć właściwość lub metodę
// obiektu, skorzystamy ze słowa delete
const car = {
   brand: 'Mercedes',
   color: 'czerwony',
   showText() {
      console.log(`${this.brand} koloru ${this.color}`);
   },
};

console.log(car.color); //czerwony
delete car.color;
console.log(car.color); //undefined
```

### Pętla po obiekcie

```js
// przy pętli po kluczach obiektu
// najczęściej stosowana jest pętla for in
const car = {
    brand: "Mercedes",
    color: "czerwony",
    showText() { ... }
}

for (const i in car) {
    console.log(i); //brand, color, showText
}

// aby popbrać wartośći kluczy
for (const key in car) {
    console.log("Klucz: ", key);
    console.log("Wartość: ", car[key]);
}

// żeby wypisać tylko klucze danego obiektu,
//  musimy przeprowadzić dodatkowe sprawdzenie
// za pomocą funkcji hasOwnProperty()
const car = {
    brand: "Mercedes",
    color: "czerwony",
    showText() { ... }
}

for (const key in car) {
    if (car.hasOwnProperty(key)) {
        console.log(key);
    }
}

// obiekty w Javascript posiadają prototypy,
// które są schowkiem dla wspólnych
// funkcjonalności danej grupy obiektów.
// Pętla for in robi pętlę po kluczach
// danego obiektu, ale także
// po kluczach prototypu danego obiektu

    function Car(name, color, speed) {
        this.name = name;
        this.color = color;
        this.speed = speed;
    }

    Car.prototype.drive = function() {
        console.log(`${this.name} sobie jedzie`);
    };

    Car.prototype.refuel = function() {
        console.log(`${this.name} zatankowany`);
    };

    Car.prototype.repair = function() {
        console.log(`${this.name} został naprawiony`);
    };

    const car1 = new Car("BMW", "black", 100);

    console.log("Pętla bez hasOwnProperty:");
    for (const key in car1) {
        console.log(key);
    }

    console.log(' ');
    console.log("Pętla z hasOwnProperty:");
    for (const key in car1) {
        if (car1.hasOwnProperty(key)) {
            console.log(key);
        }
    }

// powyższe zwróci odpowiednio
// pętla bez hasOwnProperty:
// name
// color
// speed
// drive
// refuel
// repair

// pętla z hasOwnProperty:
// name
// color
// speed
```

### Destrukturyzacja tablic

```js
// tablica
const tab = ['Ala', 'Ola', 'Ela'];

//klasycznie
const name1 = tab[0];
const name2 = tab[1];

//za pomocą destrukturyzacji
const [name1, name2] = tab;

// wyciągnięcie wartości, z pominięciem kolejnej
const tab = ['Ala', 'Ola', 'Ela', 'Fela'];
const [name1, name2, , name4] = tab;

console.log(name1, name2, name4); //"Ala", "Ola", "Fela"

// możemy ustawić domyślą wartość,
// która zostanie użyta, jeżeli w tablicy
// nie będzie wartości na danym indeksie
const tab = ['Ala', 'Ola'];
const [name1 = 'brak', name2 = 'brak', name3 = 'brak'] = tab;
console.log(name1, name2, name3); //"Ala", "Ola", "brak"

// przypisanie takie możemy też zastosować
// przy zamianie miejscami wartości zmiennych
let a = 1;
let b = 5;

[a, b] = [b, a];
console.log(a); // 5
console.log(b); // 1
```

### Destrukturyzacja obiektów

```js
// obiekt
const ob = {
   name: 'Rudzik',
   pet: 'kot',
};

//klasycznie
const name = ob.name;
const pet = ob['pet'];

//za pomocą destrukturyzacji
const { name, pet } = ob;

// tak samo jak w przypadku tablic,
// zmiennym możemy ustawić domyślą wartość
const obj = {
   first_name: 'Karol',
   last_name: 'Kowalski',
};

const { first_name = 'brak', last_name = 'brak', favoritePet = 'brak' } = obj;

console.log(first_name); //Karol
console.log(last_name); //Kowalski
console.log(favoritePet); //"brak"

// gdy chcemy stworzyć zmienne o nowych nazwach,
// trzeba użyć znaku dwukropka
const obj = {
   first_name: 'Karol',
   last_name: 'Kowalski',
};

const {
   first_name: name = 'brak',
   last_name: surname = 'brak',
   favoritePet: pet = 'brak',
} = obj;

console.log(name); //Karol
console.log(surname); //Kowalski
console.log(pet); //"brak"
```

### Destrukturyzacja w iteracji

```js
.fetch(.....)
.then(result => result.json())
.then(result => {
    //działamy na pobranych użytkownikach
    for (const el of result.users) {
        const {
            name = "",
            surname = "",
            email = "",
            plan = "basic"
            role = "user",
            www = ""
        } = el;

        console.log(surname, name, email, plan, role, www);
    }
});
```

### Destrukturyzacja i parametry funkcji

```js
//  gdy mamy obiekt lub tablicę, można
// używać desktruturyzacji do wyciągania
// danych z jego wnętrza

// Zamiast działać bezpośrednio
// na danej zmiennej
const buttons = document.querySelectorAll('button');

//zamiast
buttons.forEach((el) => {
   console.log(`Tekst elementu to ${el.innerText} a jego id to ${el.id}`);
});

// można wyciągnąć odpowiednie dane
const buttons = document.querySelectorAll('button');

buttons.forEach(({ innerText: text, id }) => {
   console.log(`Tekst elementu to ${text} a jego id to ${id}`);
});

// podobnie będzie miało to miejsce
// w przypadku przekazywania
// wartości do funkcji

// zamiast
function showUser(ob) {
   console.log(ob.name);
   console.log(ob.surname);
}

const user = {
   name: 'Marcin',
   surname: 'Nowak',
};

showUser(user);

// można
function showUser({ name, surname }) {
   console.log(name);
   console.log(surname);
}

const user = {
   name: 'Marcin',
   surname: 'Nowak',
};
showUser(user);

// w obiektach kolejność kluczy nie ma znaczenia,
// dzięki czemu mogę przekazywać do funkcji
// dane nie zważając na kolejność parametrów
function print(name, speed, color, food) {}

//mam kilka zmiennych, które chcę do niej przekazać
const name = 'Szamson';
const speed = 10000;
const color = 'brown';
const food = 'mięso';
const type = 'dog';
const profession = 'fight with bad guys';

//w przypadku zwykłej funkcji muszę pamiętać kolejność parametrów
print(name, speed, color, food);

// zamiast pamiętania kolejności, można
// skróconym zapisem stworzyć obiekt
// i przekazać go do funkcji

// ktoś przekazuje obiekt, i można go
// od razu rozbić na odpowiednie zmienne
function print({ name, speed, color, food }) {}

const name = 'Szamson';
const speed = 10000;
const color = 'brown';
const food = 'mięso';
const type = 'dog';
const profession = 'fight with bad guys';

//tworzę obiekt skróconym zapisem i przekazuję do funkcji
const ob = { name, speed, color, food };
print(ob);

//lub jeszcze krócej bez tworzenia dodatkowej zmiennej
print({ name, food, speed, color, type, profession });
```

### Destrukturyzacja i rest

```js
// operatora rest, co pozwala
// wybierać resztę zmiennych:
const tab = [1, 2, 3, 4, 5];
const [first, ...other] = tab;
console.log(first, other); //1, [2, 3, 4, 5]

// możemy też stosować dla innych obiektów,
// co przydaje się gdy chcemy
// pomijać jakieś właściwości
const ob = {
   name: 'Piotrek',
   age: 20,
   surname: 'Nowak',
   pet: 'pies',
};

const { pet, ...obWithoutPet } = ob;

console.log(pet); //"pies"
console.log(obWithoutPet); //obiekt bez właściwości pet

// inny przykład
const carData = {
   brand: 'BMW',
   color: 'red',
   maxSpeed: 260,
   owner: 'Jan Nowak',
   ownerAge: 30,
};

const { owner, ownerAge, ...car } = carData;
console.log(car); //car bez właściwości owner i ownerAge
```

### Destrukturyzacja zagnieżdżonego obiektu

```js
// jeżeli za pomocą destrukturyzacji chcemy
// wyciągać zagnieżdżone dane, wtedy w naszym
// wzorze powinniśmy odwzorować wygląd
// struktury obiektu
const myObj = {
   first_name: 'Karol',
   last_name: 'Nowak',
   role: 'driver',

   pets: ['pies', 'kot'],

   car: {
      name: 'Honda',
      year: 2002,
      type: 'hatchback',
   },
};

const {
   first_name: name,
   last_name: surname,
   role,

   pets: [pet1, pet2],

   car: { name: carName, year: carYear, type: carType },
} = myObj || {};
// powyżej wzorzec został podstawiony pod myObj lub pusty obiekt
// Dzięki czemu został zabezpieczony wypadek,
// gdyby nie było myObj w ogóle.
```

### Kopiowanie obiektów

```js
//  jeżeli pod dwie i więcej zmiennych
// podstawimy ten sam obiekt,
// będą one wskazywać na ten sam byt
const a = { name: 'kot' };
const b = a;
b.age = 5;
console.log(a, b); //{name: "kot", age: 5}, {name: "kot", age: 5}

// do kopiowania płaskich obiektów
// możemy wykorzystać spread syntax
const a = {
   name: 'kot',
   age: 3,
};

const b = { ...a };
b.name = 'pies';

console.log(a, b); //{name: "kot", age: 3}, {name: "pies", age: 3}

// inny przykład
const a = {
   name: 'kot',
   speed: 10,
};
const b = {
   name: 'pies',
   age: 5,
};

const c = { ...a, ...b };
console.log(c); //{name : "pies", speed: 10, age: 5}

// Object.assign(cel, ...źródła).
// funkcja ta służy do kopiowania
// wszystkich wyliczalnych właściwości
// z jednego lub więcej obiektów
// do obiektu docelowego
const a = {
   name: 'kot',
   age: 7,
   speed: 10,
};

const b = {
   name: 'pies',
   age: 5,
};

const c = Object.assign({}, a, b);
console.log(c); //{name : "pies", age: 5, speed: 10}

// inny przykład
const o1 = { a: 1, b: 1, c: 1 };
const o2 = { b: 2, c: 2 };
const o3 = { c: 3 };

const obj = Object.assign({}, o1, o2, o3);
console.log(obj); //{ a: 1, b: 2, c: 3 }

// spread i assign kopiuje tylko płaskie obiekty
// jeżeli któraś z właściwości wskazuje
// na inny obiekt, zostanie skopiowana
// tylko referencja do tego obiektu
const food = { type: 'rybki' };

const a = {
   name: 'kot',
   food: food,
};

const b = { ...a };
b.food.type = 'chrupki';

console.log(b.food, a.food); //{type : "chrupki"}, {type : "chrupki"}

// aby sklonować obiekt głęboko, trzeba
// użyć np. obiektu JSON
const ob = {
   name: 'Marcin',
   pet: {
      name: 'Feliks',
      kind: 'cat',
   },
};

const ob2 = JSON.parse(JSON.stringify(ob));

ob2.pet.name = 'Super Szamson';
ob2.pet.kind = 'pies';

console.log(ob.pet.name, ob2.pet.name); //Feliks, Super Szamson
console.log(ob.pet.kind, ob2.pet.kind); //cat, pies
```

### Map i Set

```js
// TODO ---------------------------------------   Map i Set
```

### Dziedziczenie w JS

```js
// TODO
```

# Konstruktor

### Tworzenie konstruktora

```js
//  konstruktor, na bazie
// którego stworzymy nowe obiekty
function Enemy(speed, power) {
   this.live = 3;
   this.speed = speed;
   this.power = power;

   this.print = function () {
      console.log(`
            Przeciwnik ma:
            życia: ${this.live}
            szybkości: ${this.speed}
            siły ataku: ${this.power}
        `);
   };
}

// tworzenie obiektu na bazie
//  nowego konstruktora
const enemy1 = new Enemy(3, 10);
enemy1.print();

const enemy2 = new Enemy(5, 15);
enemy2.print();
```

### Prototyp

```js
// podczas tworzenia obiektu automatycznie
// dostaje on właściwość __proto__
// która wskazuje na ten obiekt
const enemy1 = new Enemy(3, 10);
console.log(enemy1.__proto__ === Enemy.prototype); //true

// działa to dla każdego
// typu JS
const tabA = [1, 2, 3];
const tabB = new Array(1, 2, 3);
tabA.__proto__ === Array.prototype; //true
tabB.__proto__ === Array.prototype; //true

const txt = 'Ala ma kota';
const txtB = new String('Ala ma kota');
txtA.__proto__ === String.prototype; //true
txtB.__proto__ === String.prototype; //true
```

### Rozbudowa prototypu

```js
// prototyp jest obiektem tak więc
// można także go rozbudowywać
// jeśli coś do niego dodamy to będzie to
// dostępne dla wszystkich instacji
// już stworzonych i tworzonych w przyszłości
function Enemy(speed, power) {
   this.live = 3;
   this.speed = speed;
   this.power = power;
}

//dodajemy nowe metody do prototypu
Enemy.prototype.attack = function () {
   console.log(`Atakuje z siłą ${this.power}`);
};

Enemy.prototype.fly = function () {
   console.log(`Lecę z szybkością ${this.speed}`);
};

//tworzę nowe obiekty
const enemy1 = new Enemy(3, 10);
enemy1.attack(); //Atakuje z siłą 10
enemy1.fly(); //Lecę z szybkością 3

const enemy2 = new Enemy(5, 15);
enemy2.attack(); //Atakuje z siłą 15
enemy2.fly(); //Lecę z szybkością 5

// dodanie do prototypu
// całego obiektu
function SuperHero(name) {
   this.name = name;
}

//inna metoda ustawiania prototypu
//czy lepsza? Niekoniecznie. Można zapomnieć
// o ustawieniu niektórych rzeczy np. właściwości - constructor
SuperHero.prototype = {
   speed: 'ultra',
   strength: 90001,
   action: function () {
      return 'Ratowanie świata';
   },
};

// dzięki zastosowaniu prototypu
// oszczędzamy zasoby
function Helicopter(name) {
   this.name = name;
   this.ammo = 2000;
   this.rockets = 16;

   this.attack = function () {
      this.ammo -= 100;
      this.rockets -= 2;

      console.log(`
            Helikopter: ${this.name} atakuje
            Pozostało amunicji: ${this.ammo}
            Pozostało rakiet: ${this.rockets}
        `);
   };
}

const army = [];
for (let i = 0; i <= 1000000; i++) {
   const heli = new Helicopter('Apache' + i);
   army.push(heli);
}
// powyższy kod tworzy 1000000 obiektów
// 1000000 właściwości name, ammo, rocket
// oraz 1000000 metody attack
// gdy attack zamieścimy w prototypie
// to będzie występować tylko
// w jednym nmiejscu w pamięci
function Helicopter(name) {
   this.name = name;
   this.ammo = 2000;
   this.rockets = 16;
}

Helicopter.prototype.attack = function () {
   this.ammo -= 100;
   this.rocket -= 2;

   console.log(`
        Helikopter: ${this.name} atakuje
        Pozostało amunicji: ${this.ammo}
        Pozostało rakiet: ${this.rockets}
    `);
};

const army = [];
for (let i = 0; i <= 1000000; i++) {
   const heli = new Helicopter('Apache' + i);
   army.push(heli);
}

army[0].__proto__ === Helicopter.prototype; //true
army[500].__proto__ === Helicopter.prototype; //true
army[999999].__proto__ === Helicopter.prototype; //true
army[500].__proto__ === army[999999].__proto__; //true
```

### Rozszerzanie wbudowanych typów

```js
// możemy także modyfikować prototyp
// dla obiektów wbudowamych JS
// jednak nie polaca się takiego kodowania
String.prototype.firstCapital = function () {
   return this[0].toUpperCase() + this.substr(1);
};

String.prototype.mixLetterSize = function () {
   let text = '';

   for (let i = 0; i < this.length; i++) {
      text += i % 2 === 0 ? this[i].toUpperCase() : this[i].toLowerCase();
   }

   return text;
};

const text1 = 'marcin';
console.log(text1.firstCapital()); //wypisze Marcin

const text2 = 'marcin';
console.log(text2.mixLetterSize()); //wypisze MaRcIn
```

# Class

### Deklaracja klasy

```js
// deklaracja klasy
class Animal {
   constructor() {}
   method1() {}
   method2() {}
   method3() {}
}

//lub o wiele rzadziej spotykane
const Animal = class {
   constructor() {}
   method1() {}
   method2() {}
   method3() {}
};

//tworzymy instancje tak samo jak poprzednio
const pet1 = new Animal();
const pet2 = new Animal();

// class jest tylko innym zapisem
// w tle to i tak funkcja
class AnimalA {}
console.log(typeof AnimalA); //function

function AnimalB() {}
console.log(typeof AnimalB); //function
```

### constructor()

```js
// constructor() to funkcja odpalana automatycznie
// przy tworzeniu instancji za pomocą new
class Animal {
   constructor(name, age) {
      this.name = name;
      this.age = age;
   }

   method1() {}
   method2() {}
   method3() {}
}

const animal = new Animal('pies', 8);

// funkcja constructor() jest tym samym,
// co używana w poprzednim zapisie
// funkcja będąca konstruktorem
function PersonFn(name, age) {
   this.name = name;
   this.age = age;
}

//w nowej składni ES6
class PersonCl {
   constructor(name, age) {
      this.name = name;
      this.age = age;
   }
}
```

### Dodawanie metod

```js
// dodając nowe metody i właściwości
// do prototypu danej klasy
// nie musimy pamiętać o składni prototype.
// wystarczy, że metody te umieścimy wewnątrz klasy
// one automatycznie trafiają do prototypu
class Animal {
   constructor(name, age) {
      this.name = name;
      this.age = age;
   }

   eat() {
      console.log(this.name + ' jem');
   }

   sleep() {
      console.log(this.name + ' śpię');
   }
}
```

### Właściwości

```js
// właściwości dla danej instancji
// dodajemy wewnątrz konstruktora
class Animal {
   constructor(name) {
      this.name = name;
      this.legs = 4;
      this.type = 'animal';
   }
}

// w najnowszym JS uproszczono zapis
// i można je definiować poza konstruktorem
// równoznaczne z powyższym kodem
class Animal {
   legs = 4;
   type = 'animal';

   constructor(name) {
      this.name = name;
   }
}
```

### Metody statyczne

```js
// tworząc metody danej klasy
// trafiają one do prototypu
class Human {
   constructor(name) {
      this.name = name;
   }

   say() {
      console.log('Jestem człowiek');
   }
}

Human.say(); //błąd, bo say jest w prototypie
Human.prototype.say(); //"Jestem człowiek"

const ob = new Human('Marcin');
ob.say(); //"Jestem człowiek"

// metody możemy przypisywać do obiektów
// ala tekże do instancji obiektu
const ob = new Human('Marcin');
ob.say(); //Jestem człowiek
ob.eat = function () {
   console.log('Jem śniadanie');
};
ob.prototype.eat(); //nie ma, bo tylko powyższa instancja ma tą metodę

// metody statyczne  nie są dostępne
// dla nowych instancji,
// a tylko dla samych klas

// przykład w ES5
function Human {
    this.name = name;
}

//metoda statyczna
Human.create = function() {
   console.log("Tworzę");
}

Human.prototype.say = function() {
    console.log("Jestem człowiek");
}

const ob = new Human("Marcin");
ob.create(); //błąd
Human.create(); //"Tworzę"

// przykład w ES6
class Human {
    constructor(name) {
        this.name = name;
    }

    say() {
        console.log("Jestem człowiek");
    }

    static create() {
        console.log("Tworzę");
    }
}

const ob = new Human("Marcin");
ob.create(); //błąd
Human.create(); //"Tworzę"

// metody statyczne najczęściej wykorzystywane
// są do tworzenia użytecznych funkcji
// dla danej klasy. Można dzięki temu
// pogrupować funkcjonalności
// dotyczące danych klas w jednym miejscu
class User {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    static compareByName(a, b) {
        if (a.name < b.name) return -1;
        if (a.name > b.name) return 1;
        return 0;
    }

    static compareByAge(a, b) {
        return a.age - b.age;
    }
}

const users = [
    new User("Tomek", 10),
    new User("Ania", 35),
    new User("Beata", 20),
    new User("Monika", 20),
    new User("Karol", 22)
];

users.sort( User.compareByName );
console.log( users[0].name ); // Ania

users.sort( User.compareByAge );
console.log( users[0].name ); // Tomek

```

# Konstruktor dziedziczenie

### Dziedziczenie

```js
// tworzymy obiekt
function Enemy(name, x, y) {
   this.name = name;
   this.x = x;
   this.y = y;
   console.log('Tworzę przeciwnika: ' + this.name);
}

Enemy.prototype.fly = function () {
   return this.name + ' latam';
};

//dziedziczymy prototyp
function EnemyShoot(name, x, y) {
   this.name = name;
   this.x = x;
   this.y = y;
   this.type = 'shooter';
}

EnemyShoot.prototype = Object.create(Enemy.prototype);
//lub EnemyShoot.prototype = Object.assign({}, Enemy.prototype);
//lub EnemyShoot.prototype = Object.create(...Enemy.prototype);
EnemyShoot.prototype.constructor = EnemyShoot;

EnemyShoot.prototype.shoot = function () {
   return this.name + ' strzelam';
};

const enemyN = new Enemy('Normalny');
console.log(enemyN.fly()); //Normalny latam
console.log(enemyN.shoot()); //błąd - nie ma takiej metody

const enemyS = new EnemyShoot('Shooter');
console.log(enemyS.fly()); //Shooter latam
console.log(enemyS.shoot()); //Shooter strzelam
```

### Odwoływanie się do konstruktora ojaca: Call i apply

```js
function Enemy(name, x, y) {
   this.name = name;
   this.x = x;
   this.y = y;
   this.speed = Math.random() * 3;
   //...tutaj 20 linii skomplikowanych wyliczeń dla naszego przeciwnika...
   console.log('Tworzę przeciwnika: ' + this.name);
}

function EnemyShoot(name, x, y) {
   //tutaj chcemy odpalić kod z powyższego konstruktora Enemy
   //plus coś dodatkowego np.:
   this.type = 'shooter';
}

// aby dokonać powyższego użyjemy metody call()
function EnemyShoot(name, x, y) {
   Enemy.call(this, name, x, y); //Enemy wymaga 3 parametrów
   this.type = 'shooter';
}

const shooter = new EnemyShoot('Shooter'); //Tworzę przeciwnika: Shooter

// call jest dostępna dla każdej
// funkcji i służy do jej wywołania
function myFunc() {
   console.log('Jestem funkcją');
}
//odpalamy przez nazwę
myFunc();
//lub call
myFunc.call();

// pierwszy parametr funkcji call to wartość
// kltóra zostanie podstawiona pod this
const ob = {
   name: 'Jan',
   print() {
      console.log('Mam na imię ' + this.name);
   },
};

ob.print(); //Mam na imię Jan

const ob2 = {
   name: 'Roman',
};

//pożyczam metodę z tamtego obiektu
ob.print.call(ob2); //Mam na imię Roman
//i znowu pożyczam
ob.print.call({ name: 'Jan' }); //Mam na imię Jan

// jeżeli taka pożyczona funkcja
// wymagałaby jakiś parametrów
// to podajemy je jako kolejne
const ob = {
   name: 'x-wing',
   print(shotCount, speed) {
      console.log(
         `${this.name} strzela ${shotCount} razy z szybkością ${speed}`
      );
   },
};

const tie = {
   name: 'Tie fighter',
};

ob.print.call(tie, 5, 200); //Tie fighter strzela 5 razy z szybkością 200

// jeżeli wiemy, że w funkcji nie
// jest obsługiwane this
// to przekazujemy null lub undefined
const ob = {
   sayHiToPet(pet) {
      console.log(`Cześć ${pet} !!!`);
   },
};
ob.sayHiToPet.call(null, 'Świnka'); //Cześć Świnka!!!

// apply() działa tak samo
// ale poza obiektem this przyjmuje tylko
// jeden atrybut w postaci tablicy
// która zawiera w sobie parametry
const ob = {
   name: 'nikt',
   print(pet1, pet2) {
      console.log(
         `Nazywam się ${this.name} i mam 2 zwierzaki: ${pet1} i ${pet2}`
      );
   },
};

const user = {
   name: 'Jan',
};

ob.print.apply(user, ['pies', 'kot']); //Nazywam się Jan i mam dwa zwierzaki: pies i kot
```

### instanceof

```js
//  sprawdzanie, jakiego typu jest konkretny obiekt
const enemyN = new Enemy('Normalny');
enemyN.fly(); //Normalny latam

const enemyS = new EnemyShoot('Shooter');
console.log(enemyS.fly()); //Shooter latam i czasami strzelam!!!

console.log(enemyN instanceof Enemy); //true
console.log(enemyS instanceof EnemyShoot); //true
console.log(enemyN instanceof Object); //true
console.log(enemyS instanceof Object); //true

const ob = {
   name: 'Jan',
};

console.log(ob instanceof Object); //true
console.log(ob instanceof Enemy); //false
console.log(ob instanceof EnemyShoot); //false
```

# Class dziedziczenie

### extends

```js
class Enemy {
   constructor(name, x, y) {
      this.name = name;
      this.x = x;
      this.y = y;
      console.log('Tworzę przeciwnika: ' + this.name);
   }

   fly() {
      return this.name + ' latam';
   }
}

// dziedziczymy przez extends
// super() wywołuje kod rozszerzanej metody
class EnemyShoot extends Enemy {
   constructor(name, x, y) {
      super(name, x, y);
      this.type = 'shooter';
   }

   shoot() {
      return this.name + ' strzelam';
   }
}

// w super() przekazujemy potrzebne wartości
class Point {
   constructor(x, y) {}
}

class Dot extends Point {
   constructor(x, y, color) {
      super(x, y);
      this.color = color;
   }
}

// w przypadku rozszerzania innych metod,
// też używamy super, po której podajemy
// nazwę rozszerzanej metody
class Enemy {
   constructor(name, x, y) {
      this.name = name;
      this.x = x;
      this.y = y;
      console.log('Tworzę przeciwnika: ' + this.name);
   }

   fly() {
      return this.name + ' latam';
   }
}

class EnemyShoot extends Enemy {
   constructor(name, x, y) {
      super(name, x, y);
      this.type = 'shooter';
   }

   shoot() {
      return this.name + ' strzelam';
   }

   fly() {
      const text = super.fly();
      return text + ' i czasami strzelam!!!';
   }
}

const enemyN = new Enemy('Normal');
enemyN.fly(); //"Normal latam"

const enemyS = new EnemyShoot('Shooter');
console.log(enemyS.fly()); //"Shooter latam i czasami strzelam!!!""
```

### Klasa abstrakcyjna

```js
// klasa abstrakcyjna, to taka klasa,
// na bazie której nie powinniśmy tworzyć
// nowych instancji, a jedynie ją
// w przyszłości rozszerzać
class Animal {
   constructor(name) {
      if (this.constructor === Animal) {
         throw new Error('Nie możesz tworzyć obiektów z klasy abstrakcyjnej!');
      }
      this.type = 'animal';
      this.name = name;
   }
   eat() {
      return 'I eat food';
   }
}

//lub
class Animal {
   constructor(name) {
      if (new.target === Animal) {
         throw new Error('Nie możesz tworzyć obiektów z klasy abstrakcyjnej!');
      }
      this.type = 'animal';
      this.name = name;
   }
   eat() {
      return 'I eat food';
   }
}
```

### Rozszerzanie wbudowanych typów

```js
// np Array
class MyArray extends Array {
   constructor(...param) {
      super(...param);
   }

   sortNr() {
      return this.sort((a, b) => a - b);
   }
}

const tab1 = new Array(4, 5, 20, 21, 2.1, 1.2, 3);
tab1.sortNr(); //błąd : nie ma takiej metody

const tab2 = new MyArray(4, 5, 20, 21, 2.1, 1.2, 3);
tab2.sortNr();
console.log(tab2); //[1.2, 2.1, 3, 4, 5, 20, 21]

// lub String
class MyString extends String {
   constructor(...param) {
      super(...param);
   }
   mix() {
      return [...this]
         .map((letter, i) =>
            i % 2 === 0 ? letter.toUpperCase() : letter.toLowerCase()
         )
         .join('');
   }
}

const txt1 = new String('lubie koty i psy');
txt1.mix(); //błąd : nie ma takiej metody

const txt = new MyString('lubie koty i psy');
console.log(txt.mix()); //LuBiE KoTy i pSy
```

# DOM

## Document Object Model

### Pobieranie elementów

```js
// querySelector() zwraca pierwszy
// pasujący do selektora element, lub null
//jak nic nie znajdzie
//pobieramy pierwszy element .btn-primary
const btn = document.querySelector('.btn-primary');

//pobieramy pierwsze li listy ul
const li = document.querySelector('ul li');

//pobieram element, który ma id module
const module = document.querySelector('#module');

//  querySelectorAll() zwraca kolejcję elementów
// lub pustą kolekcję jeśli nic nie znajdzie
const buttons = document.querySelectorAll('.button');

for (const btn of buttons) {
   console.log(btn);
}

// metody te możemy odpalać dla całego dokumentu
// lub dla każdego elementu z osobna
// w całym dokumencie:
const buttons = document.querySelectorAll('.button');

// w .module
const module = document.querySelector('.module');
const buttons = module.querySelectorAll('.button');

// inne metody mniej zalecane
getElementById('id'); // pobiera jeden element o danym id
getElementsByTagName('tag-name'); // pobiera elementy o danym znaczniku
getElementsByClassName('class-name'); // 	pobiera elementy o danej klasie
getElementsByName('name'); // pobiera elementy o danym atrybucie name
```

### Pętle po kolejkach

```js
const elements = document.querySelectorAll('.module');
elements.style.color = 'red'; //błąd - bo to kolekcja
elements[0].style.color = 'red'; //ok bo pierwszy element w kolekcji

//ok, bo robimy pętlę
for (const el of elements) {
   el.style.color = 'red';
}
// w powyższym nie możemy używać metod przeznaczonych
// dla tablic ponieważ kolekcje przypominają tablice
// ale nimi nie są
const elements = document.querySelectorAll('.module');
elements.map((el) => (el.style.color = 'red')); //błąd - map jest dla tablic

// powyższe można pobejść konwertując
// kolekcję na tablicę używając
//  spread syntax lub Array.from()
onst buttons = document.querySelectorAll("button");
[...buttons].map(el => el.style.color = "red");

// wyjątkiem jest forEach którą możemy
// użuywać dla kolekcji
const elements = document.querySelectorAll(".module");

elements.forEach(el => {
    el.style.color = "blue"
});
```

### Gotowe kolekcje

```js
document.body; //element body
document.all; //kolekcja ze wszystkimi elementami na stronie
document.forms; //kolekcja z formularzami na stronie
document.images; //kolekcja z grafikami img na stronie
document.links; //kolekcja z linkami na stronie
document.anchors; //kolekcja z linkami będącymi kotwicami
// i inne
```

### Żywe kolekcje

```js
// poniższe zwracają kolekcję NodeList
querySelector();
querySelectorAll();

// poniższe zwracają kolekcję HTMLCollection
getElementsByTagName();
getElementById();
getElementsByClassName();
getElementsByName();

// NodeList i HTMLCollection

// HTMLCollection:
// nie pozwalają używać forEach();
// chyba że zamienimy je na tablice
// oraz zawierają żywe kolelcje
// tzn. np. gdy pobieramy spany w danym elemencie
// i jeśli w przyszłości liczba tych spanów się zmieni
// (dojdą nowe lub zostaną usunięte)
// kolekcja getElementsByTagName zmieni się
// kolekcja NodeList będzie jak w momencie pobrania
```

### Selektor :scope

```js
// jeżeli chcemy by działanie selektorów
// odbywało się od danego rodzica
// (tutaj .module) musimy użyć
// specjalnego selektora :scope
<div class="module">
    <div data-id="one">
        <div data-id="two"> <!-- tego chcemy złapać -->
        </div>
    </div>
</div>

const module = document.querySelector(".module");

const divTwo = module.querySelector("div div");
console.log(divTwo); //<div data-id="one"></div>

// używając :scope
const module = document.querySelector(".module");
const divTwo = module.querySelector(":scope div div");
console.log(divTwo); //<div data-id="two"></div>


```

## Właściwości elementów

### innerHTML i outerHTML

```js
// innerHTML umożliwia odczyt i ustawianie html,
// we wnętrzu danego elementu
<button class='button'>
   <span>Kliknij mnie</span>
</button>;

const btn = document.querySelector('.button');
console.log(btn.innerHTML); //<span>Kliknij mnie</span>
btn.innerHTML = '<span>Nie klikaj mnie!</span>';

// outerHTML
const btn = document.querySelector('.button');
console.log(btn.outerHTML); // <button class="button"> <span>Kliknij mnie</span></button>
```

### innerText i textContent

```js
// zwracają lub ustawiają sam tekst (bez znaczników HTML)
// innerText działa na sparsowanym tekście
// textContent na oryginalnym, wpisanym do pliku HTML
const btn = document.querySelector('.btn');
console.log(btn.innerHTML); //<span>Kliknij mnie</span>
console.log(btn.innerText); ///"Kliknij mnie"
console.log(btn.textContent); //"Kliknij mnie"

// przy dodoawaniu tekstu
// textContent - wstawi  elementu w oryginalnej postaci
// innerText - automatycznie doda nam <br>
```

### tagName

```js
// tagName zwraca nazwę elementu np. h2, a, p itp
<button class='button'>
   <span>Kliknij mnie</span>
</button>;

const btn = document.querySelector('.button');
console.log(btn.tagName); // BUTTON

// przydatne np w:
const elements = document.querySelectorAll('body *');
for (const el of elements) {
   if (el.tagName === 'STRONG') {
      el.style.border = '1px solid red';
   }
}
```

### Praca z atrybutami

```js
el.getAttribute(name); // pobiera wartość danego atrybutu null jak nie ma
el.setAttribute(name, value); // ustawia nową wartość atrybutu
el.hasAttribute(name); // sprawdza czy ma atrybut: zwraca true lub false
el.removeAttribute(name); // usuwa atrybut o danej nazwie
el.toggleAttribute(name); // dodaje/usuwa dany atrybut

// przykład
<a href='http://google.pl'> Wyszukaj </a>;
const link = document.querySelector('a');

const href = link.getAttribute('href'); //"http://google.pl"
const target = link.getAttribute('target'); //null

link.setAttribute('target', '_blank');
if (link.hasAttribute('target')) {
   console.log(link.getAttribute('target')); //"_blank"
}
```

### dataset

```js
// atrybuty dziellimy na standardowe:
// src, alt, title, class itp.
// oraz na własne
// data-text, data-direction
<div
   class='module'
   data-type='important'
   data-position='top'
   data-my-custom-data='Przykładowy tekst'
></div>;

const tooltip = document.querySelector('.module');

console.log(tooltip.dataset.type); //"important"
console.log(tooltip.dataset.position); //"top"
console.log(tooltip.dataset.myCustomData); //"Przykładowy tekst"

// przy podawaniu nazwy danego
// atrybutu pomijamy początek data-
// a myślniki w nazwie zamieniamy
// na zapis camelCase
tooltip.dataset.myCustomData = 'nowa wartość'; //utworzy w elemencie atrybut data-my-custom-data="nowa wartość"
tooltip.dataset.style = 'primary'; //utworzy atrybut data-style="primary"
tooltip.dataset.moduleSize = 'big'; //utworzy atrybut data-module-size="big"

//to samo możemy uzyskać za pomocą getAttribute i setAttribute
tooltip.setAttribute('data-custom-data', 'nowa wartość');
tooltip.setAttribute('data-style', 'primary');
tooltip.setAttribute('data-module-size', 'big');

// cokolwiek byśmy nie przetrzymywali
// w dataset, staje się to tekstem
<div data-nr1='16' data-nr2='30'></div>;
console.log(typeof div.dataset.nr1, typeof div.dataset.nr2); //"string", "string"
console.log(div.dataset.nr1 + div.dataset.nr2); //"1630"

// idealnie nadają się więc do przechowywania
// tekstów dynamicznie wstawianych
// na stronę, kawałków html,
div.dataset.type = "error";

div[data-type="error"] {
    color: red;
}
```

## Relacje między elementami

### Relacje między węzłami

```js
// przykładowy html
<div class='test-cnt'>
   <p id='text'>
      Mała
      <strong style='color:red'>Ala</strong>
      miała
      <span style='color:blue'>kota</span>
   </p>
</div>;

// poruszanie się po elementach
const p = document.querySelector('p');

//właściwości pobierające elementy html
p.parentElement; //wskazuje na nadrzędny element - div.test-cnt
p.firstElementChild; //pierwszy element w #text
p.lastElementChild; //ostatni element w #text
p.children; //[strong, span] - kolekcja dzieci elementu #text
p.children[0]; //wskazuje na 1 element - <strong style="color:red">Ala</strong>
p.nextElementSibling; //następny brat-element
p.previousElementSibling; //poprzedni brat-element

//właściwości pobierające węzły
p.parentNode; //wskazuje na nadrzędny węzeł - div.test-cnt
p.firstChild; //pierwszy node - w naszym przypadku to tekst "Mała "
p.lastChild; //ostatni node - "" - html jest sformatowany, wiec ostatnim nodem jest znak nowej linii
p.childNodes; //[text, strong, text, span] - kolekcja wszystkich dzieci - nodów
p.childNodes[0]; //"Mała"
p.nextSibling; //następny węzeł
p.previousSibling; //poprzedni węzeł
```

### Funkcja closest

```js
// element.closest("selektor-css") idąc w górę drzewa
// odnajduje najbliższy element który pasuje do selektora
<div class='module'>
   <div class='module-content'>
      <div>
         <button class='button'>Kliknij</button>
      </div>
   </div>
</div>;

const btn = document.querySelector('.button');
btn.addEventListener('click', (e) => {
   const module = btn.closest('.module');
});
```

## Tworzenie i usuwanie elementów

### Tworzenie elementu

```js
// document.createElement(tagname)
const el = document.createElement('div');

el.classList.add('element');
el.style.background = `red`;
el.style.color = '#333';
el.innerText = 'jakiś text';
```

### Wstawianie elementu do HTML

```js
// parentElement.appendChild(newElement)
// wstawi  na koniec wybranego elementu
let counter = 0;

const el = document.createElement('div');
el.classList.add('element');
el.style.background = `hsl(${Math.random() * 360}, 90%, 70%)`;
el.style.color = '#333';
el.innerText = `Nowy ${++counter}`;

const div = document.querySelector('.test-cnt');
div.appendChild(el);

// parentElement.insertBefore(newElement, element)
// wstawia nowy element przed wskazany element
<div class='test-cnt'>
   <strong>strong</strong>
   <strong>strong</strong>
</div>;

let counter = 0;

const el = document.createElement('div');
el.classList.add('element');
el.style.background = `hsl(${Math.random() * 360}, 90%, 70%)`;
el.style.color = '#333';
el.innerText = `Nowy ${++counter}`;

const div = document.querySelector('.test-cnt');
const strong = div.querySelectorAll('strong')[1]; //pobieram 2 strong

div.insertBefore(el, strong);

//  jeśli nie wspieramy  IE11
//  można używać:
// poniższych można użyać też do tekstów
parentElement.append(newElement); // wstawia tekst lub nowy element na koniec danego elementu
parentElement.prepend(newElement); // 	wstawia tekst lub nowy element na początku danego elementu
parentElement.before(newElement); // wstawia tekst lub nowy element przed danym elementem
parentElement.after(newElement); // wstawia tekst lub nowy element za danym elementem
```

### Tworzenie tekstu za pomocą createTextNode

```js
// mozna za pomocą: innerText/textContent/innerHTML/outerHTML
// lub: createTextNode - tworzy pojedynczy węzeł tekstowy
const p = document.querySelector('#testNodeText');
const btn = document.querySelector('.btn-textNodeTest');

const word1 = document.createTextNode('Psy'); //pierwsze słowo
p.append(word1);

p.append(' są '); //nie potrzebujemy tutaj referencji

const word2 = document.createTextNode('fajne'); //ostatnie słowo
p.append(word2);

btn.addEventListener('click', () => {
   console.dir(word1); //wypiszemy sobie by zobaczyć co możemy użyć
   word1.textContent = 'Koty też';
   word2.textContent = 'super!';
});
```

### insertAdjacentHTML i insertAdjacentElement

```js
// parent.insertAdjacentHTML(position, html)
// wstawia kawałek HTML na wybranej pozycji
// position może być:
beforebegin; // wstawia element przed docelowym elementem
afterbegin; // wstawia element na początku dzieci
beforeend; // wstawia element na końcu dzieci
afterend; // wstawia element za docelowym elementem

const parent = document.querySelector('div');

parent.insertAdjacentHTML('beforebegin', '<strong>element 1</strong>');
parent.insertAdjacentHTML('afterbegin', '<strong>element 2</strong>');
parent.insertAdjacentHTML('beforeend', '<strong>element 3</strong>');
parent.insertAdjacentHTML('afterend', '<strong>element 4</strong>');

// parent.insertAdjacentElement(position, newEl)
// stawia nowy element na wybranej pozycji
const parent = document.querySelector('div');

const el = document.createElement('strong');
parent.insertAdjacentElement('beforebegin', el);

//  takie samo działanie mają metody
// append(), prepend(), before() i after()
```

### Klonowanie elementów

```js
// cloneNode(deep)
// deep oznacza, czy dany element
// ma być klonowany wraz ze swoimi dziećmi
<div class='to-clone'>
   <strong>Testowy</strong>
</div>;

const el = document.querySelector('.to-clone');

const cloneEl1 = el.cloneNode();
console.log(cloneEl1); //<div class="to-clone"></div>

const cloneEl2 = el.cloneNode(true);
console.log(cloneEl2); //<div class="to-clone"><strong>Testowy</strong></div>

// cloneNode() nie klonuje
// podpiętych zdarzeń tylko sam HTML
```

### Usuwanie elementów

```js
// parentElement.removeChild(element)
// element.remove() - gdy nie interesuje nas IE11
<div class='div-test-remove'>
   <span>Element do usunięcia</span>
</div>;

const div = document.querySelector('div');
const el = div.querySelector('span');
const btn = document.querySelector('button');

btn.addEventListener('click', (e) => {
   parent.removeChild(el);

   //lub
   el.parentElement.removeChild(el);

   //lub najprościej
   el.remove();
});

// aby usunąć wszystkie dzieci danego elementu
const ul = document.querySelector('#list');

while (ul.firstChild) {
   ul.removeChild(ul.firstChild); //lub div.firstChild.remove()
}

// for robimy od końca
// ponieważ po usunięciu danego elementu,
// przestawi nam się indeks w kolekcji
const li = document.querySelectorAll('#list li');
for (let i = li.length - 1; i <= 0; i++) {
   li[i].remove();
}

// powyższe sprawdza się tylko
// coś zrobić z usuniętymi elementami
// np odpiąć im zdarzenia
// bo można prościej
const ul = document.querySelector('#list');
//dowolne z poniższych
ul.innerHTML = '';
ul.textContent = '';
ul.innerHTML = '';
```

### Usuwanie z html i pamięć

```js
// ????????????????????
// removeChild() i remove()
// usuwają elementy z HTML, ale jeżeli
// taki element jest podstawiony pod zmienną,
// po usunięciu dalej będzie ona
// przetrzymywać dany element w pamięci.
```

### Zastępowanie elementów

```js
// parent.replaceChild(newChild, oldChild)
<div class="div-test-replace">
    <span>Jestem starym elementem</span>
</div>

<button type="button" class="button" id="replaceTest">
    Zastąp spana nowym elementem
</button>

const div = document.querySelector(".div-test-replace")
const btn = document.querySelector("#replaceTest");

btn.addEventListener("click", e => {
    const oldItem = div.querySelector("span");

    const newItem = document.createElement("strong");
    newItem.innerText = "Jestem nowym elementem";

    div.replaceChild(newItem, oldItem);
});

// inną do zastąpienia jest
// element.replaceWith(otherEl)
const span = document.querySelector(".old");

const strong = document.createElement("strong");
strong.innerText = "Zamiennik";

span.replaceWith(strong);
```

### Tworzenie fragmentów dokumentu za pomocą template

```js
// TODO
```

## CSS i Javascript - CSSOM (The CSS Object Model)

### classList

```js
// element.classList() udostępnia nam kilka metod
add(string); // dodawanie klasy lub kilku klas
remove(string); // usuwanie klasy lub kilku klas
toggle(string, *force); // przełączanie (jak nie ma to dodaje, jak jest to usuwa) klasy. Dodatkowy drugi parametr wymusza dodanie (jeżeli jest true) lub usunięcie (jeżeli jest false) klasy.
contains(string); // sprawdza czy element ma taką klasę

el.classList.add("btn");
el.classList.add("btn", "btn-primary", "inna-klasa");
el.classList.remove("btn", "inna-klasa");
el.classList.toggle("btn"); //dodaję jak nie ma, usuwam jak już jest
el.classList.toggle("btn", true); //dodaję
el.classList.contains("btn"); //true bo powyżej dodałem tą klasę

// className
element.className = "button button-big button-important";
element.className += " inna-klasa inna-klasa2";
```

### style

```js
btn.style.backgroundColor = '#4BA2EA';
btn.style.fontSize = '1.6rem';
btn.style.borderRadius = '3rem';
btn.style.color = '#F7F781';

console.log('Kolor przycisku to: ', btn.style.backgroundColor);
console.log('Kolor tekstu to: ', btn.style.color);
console.log('A wielkość tekstu to: ', btn.style.fontSize);

//lub
el.style['font-size'] = '1rem';
el.style['background'] = 'linear-gradient(#fff, #ddd)';
el.style['background-color'] = 'rgba(255,255,255,0.5)';

// cssText
el.style.cssText = `
    color: red;
    background: blue;
    padding: 10px;
`;
```

### getComputedStyle()

```js
// TODO
```

### setProperty() i getPropertyValue()

```js
// setProperty(propertyName, value, priority*)
// służy do ustawiania stylowania. Ostatni
// opcjonalny parametr priority służy do
// ewentualnego dodania deklaracji !important.
// Najczęściej jest pomijany.

// getPropertyValue(property)
// służy do pobierania stylowania
document.body.style.setProperty('background-color', '#4BA2EA');
document.body.style.setProperty('font-size', '1.5rem');

document.body.style.getProperty('background-color');
document.body.style.getProperty('font-size');

// Metody te mają jednak zastosowanie
// przy pracy ze zmiennymi css
el.style.setProperty('--size', '1em');
el.style.getPropertyValue('--size'); //"1em"

// a jeżeli połączymy to z pobieraniem
// przeliczonych styli, zmienne takie stają
// się swoistą furtką, która może
// łączyć css z Javascriptem
const size = getComputedStyle(element).getPropertyValue('--size');
element.setProperty('--size:', `{++size}`);
```

## Zdarzenia - Events

### Nasłuchiwanie zdarzeń

```js
//możemy podpiąć klasyczną funkcję anonimową
const btn = document.querySelector('.button');

btn.addEventListener('click', function () {
   console.log('Kliknąłem na element A');
});

//lub funkcję strzałkową
const btn = document.querySelector('.button');
btn.addEventListener('click', () => {
   console.log('Kliknąłem na element B');
});

//lub podpiąć funkcję poprzez referencję do niej
function showText() {
   console.log('Kliknąłem na element C');
}

const btn = document.querySelector('.button');
btn.addEventListener('click', showText);

// odpięcie nasłuchiwania zdarzenia
// element.removeEventListener()
const btn = document.querySelector('.button');

function elementClick() {
   console.log('Kliknąłem na element');
}

btn.addEventListener('click', elementClick);
btn.removeEventListener('click', elementClick);
```

### Wkraczamy w głąb zdarzenia

```js
// funkcji nasłuchującej możemy ustawić parametr
// najczęściej stosowane e lub event
// jest to dodatkowy obiekt z informacjami
// związanymi z tym zdarzeniem
// np pozycja kursora, który klawisz wciśnięty itp
element.addEventListener('click', (e) => {
   console.log(e);
});
```

### Wstrzymanie domyślnej akcji

```js
// iektóre elementy na stronie
// mają swoje domyślne akcje
// e.preventDefault() - zpobiega wykonaniu domyślnej akcji
//jeżeli chcemy robić walidację formularzy
form.addEventListener('submit', (e) => {
   e.preventDefault();
   console.log('ten formularz się nie wyśle');
});

//jeżeli chcemy kombinować z tym co wpisuje użytkownik
input.addEventListener('keydown', (e) => {
   e.preventDefault();
   console.log('w ten input nic nie wpiszesz');
});

//jeżeli chcemy robić bajerancką nawigację
link.addEventListener('click', (e) => {
   e.preventDefault();
   console.log('Ten link nigdzie nie przeniesie.');
});
```

### Zachowanie zdarzeń

```js
// faza capture - kiedy event podąża w dół drzewa
// faza target - kiedy event dotrze do elementu, który wywołał to zdarzenie
// faza bubbling - kiedy event pnie się w górę drzewa aż dotrze do window
btn.addEventListener("click", e => {...}, true); //capturing
btn.addEventListener("click", e => {...}); //bubbling

// można przekazać także obiekt
// z kilkoma własnościami
element.addEventListener("click", doSomething, {
    capture: false, //czy używać fazy capture
    once: true, //po pierwszym odpaleniu nasłuchiwanie zostanie usunięte - czyli dane nasłuchiwanie zadziała tylko 1x
    passive: false //jeżeli true, funkcja nigdy nie odpali preventDefault() nawet jeżeli podano je w funkcji
    signal : //pozwala dodać obiekt typu AbortController, dzięki któremu dana funkcja zostanie automatycznie usunięta w momencie wywołania funkcji abort()
});
```

### Zatrzymanie propagacji

```js
// aby przerwać powyższą wędrówkę (propagację)
// używamy e.stopPropagation()
<div class='parent'>
   <button class='button'>Kliknij mnie i sprawdź w konsoli</button>
</div>;

const div = document.querySelector('.parent');
const btn = document.querySelector('.parent .button');

div.addEventListener('click', (e) => {
   console.log('Kliknięto div');
});

btn.addEventListener('click', (e) => {
   e.stopPropagation();
   console.log('Kliknięto przycisk');
});

//stopImmediatePropagation()
// działa jak powyższa ale dodatkowo
// zatrzyma wywołanie reszty funkcji
// nasłuchujących dany rodzaj zdarzenia.
// poniżej różnice

// stopPropagation()
divGrandfather.addEventListener('click', (e) => {
   console.log('Kliknąłeś na grandfather');
});

divParent.addEventListener('click', (e) => {
   e.stopPropagation();
   console.log('Kliknąłeś na parent A');
});

divParent.addEventListener('click', (e) => {
   console.log('Kliknąłeś na parent B');
});

divParent.addEventListener('click', (e) => {
   console.log('Kliknąłeś na parent C');
});

button.addEventListener('click', (e) => {
   console.log('Kliknąłeś na button');
});

// WYNIK NA KONSOLI:
// Kliknąłeś na button
// Kliknąłeś na parent A
// Kliknąłeś na parent B
// Kliknąłeś na parent C

// stopImmediatePropagation()
divG.addEventListener('click', (e) => {
   console.log('Kliknąłeś na grandfather');
});

divP.addEventListener('click', (e) => {
   e.stopImmediatePropagation();
   console.log('Kliknąłeś na parent A');
});

divP.addEventListener('click', (e) => {
   console.log('Kliknąłeś na parent B');
});

divP.addEventListener('click', (e) => {
   console.log('Kliknąłeś na parent C');
});

button.addEventListener('click', (e) => {
   console.log('Kliknąłeś na button');
});

// WYNIK NA KONSOLI:
// Kliknąłeś na button
// Kliknąłeś na parent A
```

### Element nasłuchujący i ten, na którym odpalono zdarzenie

```js
//  e.target wskazuje na element,
// na którym dane zdarzenie się wydarzyło
// e.currentTarget wskazuje na element,
// do którego podpięliśmy funkcję
// nasłuchującą dane zdarzenie.

<div class='parent' id='parentTarget'>
   <button class='button' type='button'>
      Test targeta
   </button>
</div>;

const parent = document.querySelector('.parent');
parent.addEventListener('click', (e) => {
   console.log('e.target: ', e.target);
   console.log('e.currentTarget: ', e.currentTarget, parent);
});
```

### Problem ze zdarzeniami i dynamicznymi elementami

```js
// zdarzenie do dynamicznie tworzonego elementu
// musimy podpinać przy dodawaniu tego elementu


<div class="elements-list">
    <!-- tutaj trafią nowe elementy -->
</div>

<div class="add-element-bar">
    <button type="button" class="btn add-element">
        Dodaj element
    </button>
</div>

// dzialajacy kod
let counter = 0;
const addBtn = document.querySelector(".add-element");
const list = document.querySelector(".elements-list");


addBtn.addEventListener("click", e => {
    counter++;
    const el = document.createElement("div");
    el.classList.add("element");
    el.innerText = "To jest element " + counter;

    const del = document.createElement("button");
    del.innerText = "Usuń";
    del.classList.add("delete");
    del.addEventListener("click", e => {
        del.closest(".element").remove();
    });
    el.appendChild(del);

    list.appendChild(el);
});

// problem z powyższym jest taki że
// Jeżeli będziemy mieli milion takich elementów,
// to podepniemy milion funkcji nasłuchujących
// dlatego zamiast podpinać zdarzenie usunięcia
// pod przycisk podepniemy się pod rodzica
// i za pomocą e.target wewnątrz funkcji
// będziemy sprawdzać jaki element został kliknięty

list.addEventListener("click", e => {
    //e.target - ten który kliknęliśmy
    //e.currentTarget - ten któremu podpięliśmy addEventListener (czyli list)

    //sprawdzam czy kliknięty element jest przyciskiem i ma klasę .delete
    if (e.target.classList.contains("delete")) {
        e.target.closest(".element").remove();
    }
});

```

### Inne sposoby rejestrowania zdarzeń

```js
const element = document.querySelector('#button');

element.onclick = function () {
   console.log('Kliknięto element');
};

element.onmouseover = function () {
   console.log('Najechano na przycisk');
};

// aby usunąć wcześniej przypisane
// w ten sposób zdarzenie
element.onclick = null;

// problem z powyższym sposobem polega na tym,
// że do jednego elementu dla pojedynczego
// zdarzenia możemy podpiąć tylko jedną funkcję

// nie zawsze jest to problem
// często można założyć, że nie będzie
// potrzeby podpinać dodatkowych
// funkcjonalności dla danego elementu np:
const xhr = new XMLHttpRequest();
xhr.onload = function() { ... }
xhr.onerror = function() { ... }
xhr.send(null);

const form = document.querySelector("form");
form.onsubmit = function() { ... }

```

## Events - klawisze

### keyDown, keyUp, keyPress

```js
keyDown; //naciśnięcie klawisza
keyUp; //puszczenie klawisza
keyPress; //naciśnięcie i puszczenie klawisza
```

### Który klawisz został naciśnięty

```js
e.altKey; // Czy klawisz Alt jest naciśnięty
e.ctrlKey; // Czy klawisz Ctrl jest naciśnięty
e.shiftKey; // Czy klawisz Shift jest naciśnięty
e.keyCode; // Zwraca kod klawisza

const textarea = document.querySelector('#keyTest');

textarea.addEventListener('keyup', (e) => {
   const keys = [];

   if (e.shiftKey) {
      keys.push('shift');
   }
   if (e.altKey) {
      keys.push('alt');
   }
   if (e.ctrlKey) {
      keys.push('ctrl');
   }
   keys.push(e.key);

   console.log('Naciśnięte klawisze: ' + keys.join(' + '));

   if (e.keyCode >= 48 && e.keyCode <= 57) {
      console.log('klawisz to cyfra');
   }
});
```

### Blokowanie wpisywania

```js
// ustawiamy wpisywanie tylko liczb
const input = document.querySelector('input');

input.addEventListener('beforeinput', (e) => {
   e.currentTarget.previousValue = e.currentTarget.value;
});

input.addEventListener('input', (e) => {
   if (/^\d*$/g.test(e.currentTarget.value)) {
      //tylko liczby
   } else {
      e.currentTarget.value = e.currentTarget.previousValue;
   }
});
```

## Events - myszka

### mousedown, mouseup, click

```js
element.addEventListener("mousedown", e => {...});
element.addEventListener("mouseup", e => {...});
element.addEventListener("click", e => {...});
```

### mouseover, mousemove, mouseout

```js
element.addEventListener("mouseover", e => {...});
element.addEventListener("mousemove", e => {...});
element.addEventListener("mouseout", e => {...});
```

### mouseenter, mouseleave

```js
// różnią się one tym od swoich braci,
// że nie są odpalane dla dzieci danego elementu
element.addEventListener("mouseenter", e => {...});
element.addEventListener("mouseleave", e => {...});
```

### Dodatkowe informacje

```js
// aby pobrać dodatkowe informacje o zaistniałym zdarzeniu
const element = document.querySelector('.element');
element.addEventListener('click', (e) => {
   console.log(e); //MouseEvent
});
```

### Pozycja kursora

```js
e.pageX  e.pageY; // pozycja X, Y kursora od górnego lewego narożnika strony
e.clientX e.clientY; // pozycję X, Y kursora od lewej krawędzi widocznego obszaru strony (bez uwzględnienia pozycji przewinięcia strony)
e.screenX e.screenY; // Zwraca pozycję X, Y na ekranie monitora (jeżeli masz wiele ekranów to od lewego górnego rogu ekranu leżącego najdalej po lewej stronie)
e.layerX e.layerY; // Zwraca pozycję X, Y na warstwie renderowania. Nie są to standardowe właściwości
e.offsetX e.offsetY; // Zwraca pozycję X, Y kursora na od lewego górnego narożnika danego elementu
x y; // W nowych wersjach przeglądarek są to aliasy dla clientX i clientYs
```

### Który przycisk myszki

```js
// 0 - prawy przycisk myszy
// 1 - środkowy przycisk myszy
// 2 - prawy przycisk myszy
const btn = document.querySelector('.btn');
btn.addEventListener('mousedown', (e) => {
   console.log(e.button);
});
```

### Wywołanie powszechnych zdarzeń

```js
// metody służące do wywołania danego zdarzenia
// na danych elementach
element.click(); //kliknęliśmy w element
element.select(); //zaznaczamy element (tekst w inpucie)
element.focus(); //wybieramy element (jak za pomocą klawiatury)
element.blur(); //opuszczamy element
form.submit(); //wysyłamy formularz
form.reset(); //resetujemy formularz

const button = document.querySelector('button');
button.addEventListener('click', (e) => {
   console.log('klik!!!');
});

button.click();
```

### Event

```js
// konstruktor Event służy do tworzenia
// nowego zdarzenia
let btn = document.querySelector('.btn');

 btn.addEventListener('eventName', function () {
        console.log('Naciśnięto');
 });

let clickEvent = new Event('eventName'); // tworzymy zdarzenie
btn.dispatchEvent(clickEvent); // wywołujemy zdarzenie

// do konstruktora możemy przekazać dodatkowy obiekt
// który pozwala ustawić cechy danego zdarzenia
const event = new Event("load", {
    "bubbles"    : false, //czy zdarzenie ma iść w górę dokumentu
    "cancelable" : false  //czy można je zatrzymać,
    "composed"   : false //czy dane zdarzenie będzie podążać z shadow DOM do DOM
});

// wyróżniamy też zdarzenia dla:
// MouseEvent
// KeyboardEvent
// InputEvent
// ... i inne
const event = new MouseEvent("click", {
    bubbles: true,
    cancelable: true,
    clientX: 200,
    clientY: 200
});

console.log(event.clientX); // 200
```
