# TERMINAL

<br>

## Komendy

```
. --> katalog w którym się znajdujemy
.. --> katalog powyżej
sudo - prawa administratora root-a ( superuser do )
sudo apt install --> installs package
sudo apt remove --> removes package
rm -rf nazwa_folderu
cat nazwa_pliku
touch nazwa_pliku
vim nazwa_pliku
cp nazwa_pliku_1 nazwa_pliku_2
mv --> przenoszenie pliku lub zmiana nazwy pliku
pwd --> print working directory
less plik.txt --> możemy przeglądać plik page down i page up, 'q'  wychodzimy
less -N plik --> linie będą numerowane
whoami
cd --> change directory
cd nazwa_folderu
cd ..
cd ~ --> katalog user
cd --> katalog user
cd / - root
logout or exit
clear - clear terminal
Ctrl + L - clear terminal
cp -r ./doc ./dokumentacja  - kopiuje folder doc do folderu dokumentacja
cp -r ./doc/. ./dokumentacja   - kopiuje pliki z doc do folderu dokumentacja
cp *.* ~/Picture --> skopiuj wszystkie pliki do katalogu
lsblk --> list block devices
Tab --> autocomplition
unzip plik.zip --> rozpakowanie pliku
cp --help --> wyświetla pomoc
man komenda --> wyświetla manual dla komendy
echo --> wyświetla np zmienne i może wpisywać do pliku
mkdir --> twoży katalog
mkdir -p src/edu --> stwoży katalogi
ls nazwa_katalogu --> wyświetli co jest w katalogu
ls .. --> parent directory
```

```
cal --> wyświetl kalendarz
date --> wyświetl datę
```

Kopiowanie na serwer?

```
rsync -av . root@169.99.146.57:~/superowsame.com
```

Ctrl + Backspace --> usówa cełe słowo
Ctrl + strzałki --> przeskakuje słowa
<br>
<br>
<br>
<br>
<br>
<br>

## Log as root i WSL

Uruchamiamy Windows command prompt

Logowanie na root-a

```
ubuntu2004 config --default-user root
```

Logowanie na user-a

```
ubuntu2004 config --default-user marmax
```
