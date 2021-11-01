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
rm -i --> żądaj potwierdzenia
rm -v --> potwierdz operację
cat nazwa_pliku
touch nazwa_pliku
touch nazwa\ pliku.txt --> nazwa pliku z spacją
vim nazwa_pliku
cp nazwa_pliku_1 nazwa_pliku_2
mv --> przenoszenie pliku lub zmiana nazwy pliku
mv 1.txt 2.txt nazwa_folderu
pwd --> print working directory
less plik.txt --> możemy przeglądać plik page down i page up, 'q'  wychodzimy
less -N plik --> linie będą numerowane
whoami
cd --> change directory
cd nazwa_folderu
cd .. --> do poprzedniego katalogu
.. --> do poprzedniego katalogu
cd ~/projekty --> katalog user
cd ~ --> katalog user
cd --> katalog user
cd / - root directory
/ - root directory
ln --> shortcuts do innych plików ( odnośniki)
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
echo --> Wyświetl wiadomość
echo --> wyświetla np zmienne i może wpisywać do pliku
echo $HOME --> wyświetli ścieżkę domową
mkdir --> twoży katalog
mkdir -p src/edu --> stwoży katalogi
ls nazwa_katalogu --> wyświetli co jest w katalogu
ls .. --> parent directory
ls -l
ls -la
ls -lh --> pokaże KB, MB
ls | grep md --> wyświetli wszystkie pliki z rozszeżeniem md
ls | grep -i md --> nie zwraca uwagi na wielkość liter
ls *.md --> wyświetl pliki md
ls S* --> wyświetl wszystkie pliki i foldery zaczynające się od S
ls | sort --> sortuje listing
file zazwa_pliku --> sprawdzamy rodzaj pliku
```

```
cal --> wyświetl kalendarz
date --> wyświetl datę
find / -name "SSH.md"
find /home -name "SSH.md"
```

Kopiowanie na serwer?

```
rsync -av . root@169.99.146.57:~/superowsame.com
```

Ctrl + Backspace --> usówa cełe słowo
Ctrl + strzałki --> przeskakuje słowa
<br>
whoami --> sprawdzamy na kogo jesteśmy zalogowani
su root --> zaloguj się na roota
su user --> zaloguj się na user
passwd --> zmień hasło dla zalogowanego usera
passwd user --> zmień hasło dla user
id --> user id ( root - 0; user np 1000 )
<br>
<br>
<br>
<br>
<br>

## Log as root in Powershell

Uruchamiamy Powershell i logujemy się na root-a

```
wsl -u root
passwd --> zmiana hasła
```

## Logowanie w WSL

Logowanie na roota

```
su root
```

Logowanie na user-a

```
su user
```

sudo adduser nazwa

groupmode + 2xTab

sudo userdel nazwa
sudo userdel -r nazwa --> usunie równięż katalog w home

~. -->Get out of hung terminal - ssh

---

scp source_file_path destination_file_path
scp -r test backup

Kopiuje pliki z katalogu do katalogu

```
rsync -r test/ backup/
```

Kopiuje katalog do katalogu

```
rsync -r test backup/
```

Przeprowadza symulację kopiowania, wyświetli pliki nie z kopiowane

```
rsync -av --dry-run test/ backup/
```

Kopiowanie na serwer

```
rsync -zaP ~/projects/my_sites root@192.32.54.100:~/public/
```

-  z - to compress
-  a - to archive
-  P - to show the progress

Lub za pomocą

```
scp -r app root@192.32.54.100:~/public/
```
