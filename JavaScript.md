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
