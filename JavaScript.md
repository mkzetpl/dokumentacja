# JS

## 1. Okna dialogowe

```js
alert('treść komunikatu'); // OK - nic nie zwraca
confirm('treść komunikatu'); // OK - true, ANULUJ - false
prompt('treść komunikatu', 'domyślna wartość'); // ANULUJ - false, OK - wpisana wartość
```

## 2. Zmienne

### a. Deklaracja zmiennych

```js
var a = 20; // nie zalecane w użyciu, zasięg funkcyjny
let b = 20; // zasięg blokowy
const c = 20; // stała, zasięg blokowy
```

### b. Typy zmiennych

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

```

Array

```js
//Array:
let owoce = ['Jabłko', 'Banan']; // lub jak poniżej
let owoce = new Array('Jabłko','Banan');

console.log(owoce.length);// 2
let pierwszy = owoce[0]; // Jablko

owoce.forEach(function(item, index, array) {
  console.log(item, index);
});
// Jablko 0
// Banan 1

let a = owoce.push('Pomarańcz'); // ['Jabłko', 'Banan', 'Pomarańcz'], a=3 - ile elementów jest w tablicy
let b = owoce.pop(); // usuwa pomarańczę z końca // ['Jabłko', 'Banan']; b=Pomarańcz
let c = owoce.shift(); // usuwa jabłko z początku // ['Banan'], c=Jabłko
let d = owoce.unshift('Truskawki') // dodaje na początku // ['Truskawki','Banan'], d=2 - ile elementów jest w tablicy
let pos = owoce.indexOf('Banan'); // pos=1, zwraca indeks elementu tablicy

owoce.splice(pos, count); // usuwa zaczynając od pos, count - ile usunąć
let owoce = ['Jabłko', 'Banan','Mango','Sliwka','Gruszka'];
let tab = owoce.splice(1,3); // owoce: ['Jabłko','Gruszka'], tab:['Banana','Mango', 'Sliwka']

// Array.isArray()
const tab = ["ala", "bala"];
const ob = { name : "Piotr" };

console.log(Array.isArray(tab)); //true
console.log(Array.isArray(ob)); //false

console.log(typeof tab); //"object";
console.log(typeof ob); //"object";

// join() - scalanie tablicy w tekst
onst ourTable = ["Marcin", "Ania", "Agnieszka"];
console.log(ourTable.join()); //wypisze się "Marcin,Ania,Agnieszka"
console.log(ourTable.join(" - ")); //wypisze się "Marcin - Ania - Agnieszka"
console.log(ourTable.join(" <--> ")); //wypisze się "Marcin <--> Ania <--> Agnieszka"

// Zamiana tekstu na tablicę
const txt = "kartofel";
const tab = [...txt];
console.log(tab); //["k", "a", "r", "t", "o", "f", "e", "l"]

const txt = "Ala ma kota";
const tab = txt.split(" ");
console.log(tab); //["Ala", "ma", "kota"];

// reverse() - odwracanie kolejności elementów tablicy
const tab = [1, 2, 3, 4];

console.log("Przed: " + tab); //Przed: [1, 2, 3, 4]
tab.reverse()
console.log("Po: " + tab); //Po: [4, 3, 2, 1]

const word = "kajak";
const tab = [...word];
console.log(tab.reverse().join("") === tab.join("")); //true czyli palindrom

//indexOf(), lastIndexOf() i includes() wyszukiwanie elementu w tablicy

//Zwraca index szukanego tekstu lub -1 jeśli nie znajdzie
const tab = ["Marcin", "Ania", "Agnieszka", "Monika"];
let a = tab.indexOf("Agnieszka"); // a=2
let b = tab.indexOf("Genowefa"); // a=-1

// lastIndexOf() zwraca ostatnią pozycję szukanego tekstu
const tab = ["Agnieszka", "Marcin", "Ania", "Agnieszka", "Monika"];
const index = tab.lastIndexOf("Agnieszka"); // index=3

// includes() zwraca prawdę lub fałsz
//w zależności czy szukana wartość znajduje się w tablicy

const tab = ["Marcin", "Ania", "Agnieszka", "Monika"];
let a = tab.includes("Ania"); // true
let b = tab.includes("Henryk"); // false

// sort() - sortowanie tablicy
// TODO

// concat() - łączenie dwóch tablic
// TODO

// slice() - zwracanie kawałka tablicy
// TODO

// fill() - wypełnianie tablicy
// TODO

// # Pętla po tablicy
// TODO

// Tablice wielowymiarowe
// TODO


// flat() - spłaszczanie tablicy wielowymiarowej
// TODO

// Array.from()
// TODO


```

## 3. Operatory

### a. Operatory dodawania, odejmowania, mnożenia, dzielenia

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

### b. Operatory przypisania

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

### c. Operatory porównania

```js
// TODO
```

### d. Operatory logiczne

```js
// TODO
```

### e. Operatory logiczne w równaniach

```js
// TODO
```
