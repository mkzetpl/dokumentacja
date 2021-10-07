# SSH - secure shell

<br>
Składnia

```
shh {user}@{host}
```

Wklejamy publiczny klucz z naszego koputera na serwer.

```
ssh-copy-id root@46.41.143.70
```

Lub kopiujemy klucz publiczny SSH Key do clipbordu za pomocą kodu i wklejamy w panelu klienta.

```
pbcopy < ~/.ssh/id_rsa.pub
```

<br><br><br><br>

## Generowanie nowych kluczy rsa

Przechodzimy do katalogu .ssh

```
cd ~/.ssh
```

Generujemy klucze - publicznego i prywatnego

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- zmieniamy nazwe np na /Users/marmax/.ssh/id_rsa_digitalocean
- możemy wprowadzić dodatkowe hasło ale nie musimy

Możemy zkopiować do schowka publiczny klucz i wkleić np w digital ocean

```
pbcopy < ~/.ssh/id_rsa_digitalocean.pub
```

Logujemy się na serwer i otwieramy plik

```
vim ~/.ssh/authorized_keys
```

Wklejamy klucz i zapisujemy zmiany

Jak mamy wiele kluczy to musimy go dodać

```
ssh-add ~/.ssh/id_rsa_digitalocean
```

<br><br>
