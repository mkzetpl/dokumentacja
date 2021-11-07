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
// TODO
```

### Operatory logiczne

```js
// TODO
```

### Operatory logiczne w równaniach

```js
// TODO
```

# Instrukcje warunkowe

```js
// TODO
```

# Pętle for i while

```js
// TODO
```

# Number i Math

```js
// TODO
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
// TODO
```

# Funkcja strzałkowa

```js
// TODO
```

# Spread i rest

```js
// TODO
```
