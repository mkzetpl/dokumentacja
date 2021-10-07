# TERMINAL

<br>

## Komendy

```
sudo - prawa administratora root-a
rm -rf nazwa_folderu
cat nazwa_pliku
touch nazwa_pliku
vim nazwa_pliku
cp nazwa_pliku_1 nazwa_pliku_2
pwd
whoami
cd nazwa_folderu
cd ..
cd ~ - katalog user
cd / - root
logout or exit
clear
cp -r ./doc ./dokumentacja  - kopiuje folder doc do folderu dokumentacja
cp -r ./doc/. ./dokumentacja   - kopiuje pliki z doc do folderu dokumentacja
```

Kopiowanie na serwer?

```
rsync -av . root@169.99.146.57:~/superowsame.com
```

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
