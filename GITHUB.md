# GITHUB

<br>

## 1. Istalacja git-a

```
apt install git
```

<br>

## 2. Połączenie SHH z Github-em

Kopiujemy klucz publiczny

```
pbcopy < ~/.ssh/id_rsa.pub
```

Wklejamy klucz w panelu github-a

```
Settings -> SSH -> New SSH key
```

<br>

## 3. Logujemy się na githuba

<br>

## 4. Tworzymy nowe repozytorium

- Możemy utwożyć przy tworzeniu projektu plik README.md

<br>

## 5. Klonujemy repozytorium z githuba na dysk

```
git clone git@github.com:mkzetpl/dokumentacja.git
or
git clone https://github.com/mkzet/dokumentacja.git
```

<br>
<br>
<br>
<br>

# Komendy git-a

Sprawdzamy czy jakieś pliki zostały zmienone

```
git status
```

Sprawdzamy co zostało zmienione

```
git diff
```

Dodajemy zmieniony plik do paczki

```
git add index.html
```

Dodajemy wszystkie zmienione plik do paczki

```
git add .
```

Zamykamy zmienione pliki w paczce i nadajemy etykietę

```
git commit -m "Dodanie pliku index.html"
```

Przesyłamy paczkę do github-a

```
git push
```

Pobieranie aktualnego reposytorium z github-a

```
git pull
```

<br>
<br>
<br>
<br>

# Branching

Pobieranie aktualnego reposytorium z github-a

```
git pull
```

Wyswietlenie brancha

```
git branch
```

Stworzenie brancha

```
git branch nazwa_brancha
```

Przejście na brancha

```
git checkout nazwa_brancha
```

Stworzenie i przejscie na brancha

```
git checkout -b nazwa_brancha
```

Przesyłamy brancha do github-a

```
git push
or
git push orgin nazwa_brancha
```

Łączy maina do brancha w którym jesteśmy ?

```
git merge main
```

<br>
<br>
<br>
<br>

# Contributing To Open Source

## 1. Fork

- klikamy fork w projekcie na githubie
- kopiuje cały projekt i wgrywa go do naszego konta na githubie

## 2. Klonujemy repozytorium

```
git clone ssh
or
git clone https://github.com/mkzet/dokumentacja.git
```

## 3. Tworzymy nowego brancha

```
git checkout -b test
```

## 4. Wprowadzamy zmiany i wysyłamy do brancha na naszym github-ie

```
git status
git add .
git commit -m "added my name to contributors"
git push orgin test
```

## 5. Klikamy New pull request na branchu test

## 6. Keeping Your Fork Up To Date

```
git remote -v
git remote add upstream https://github.com/zero-to-mastery/PROJECT_NAME.git
git remote -v
git pull upstream master

```
