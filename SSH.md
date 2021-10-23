# SSH - secure shell

<br>

## Składnia

```
shh {user}@{host}
```

## Wklejamy publiczny klucz z naszego koputera na serwer

```
ssh-copy-id root@40.40.140.70
```

## Kopiujemy klucz i wklejamy np. w GITHUB-ie

```
cat ~/.ssh/id_rsa.pub
```

<br><br>

## Generowanie nowych kluczy i dodanie na serwer

Przechodzimy do katalogu .ssh

```
cd ~/.ssh
```

Generujemy klucze - publicznego i prywatnego

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

-  zmieniamy nazwe np na /Users/marmax/.ssh/id_rsa_digitalocean
-  możemy wprowadzić dodatkowe hasło ale nie musimy

Logujemy się na serwer i otwieramy plik

```
vim ~/.ssh/authorized_keys
```

Wklejamy klucz i zapisujemy zmiany

<br><br>

## Zarządzanie wieloma kluczami

Outputs the environment variables you need to have to connect to it:

```
ssh-agent
```

Starts ssh-agent and configures the environment in memory

```
eval $(ssh-agent -s)
```

Dodanie klucza do agenta

```
ssh-add ~/.ssh/id_rsa_digitalocean
```

Wyświetlenie używanych kluczy

```
ssh-add -l
```

<br><br>
