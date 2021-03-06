# POSTGRESQL

Aktualizacja bibliotek

```
sudo apt update
```

Instalacja PostgreSQL

```
sudo apt install postgresql postgresql-contrib
```

Logowanie jako postgres user

```
sudo -i -u postgres
```

Uruchomienie interfejsu postgres

```
psql
```

Zalogowanie się i uruchomienie interfejsu

```
sudo -u postgres psql
```

Wylogowanie z postgresa

```
exit
```

Dodanie nowego użytkownika (podajemy nazwę użytkownika np. mkzetpl)

```
sudo -u postgres createuser --interactive
```

Tworzenie nowej bazy danych

```
sudo -u postgres createdb nazwa_bazy
```

Aby zalogować się do bazy jako nowy użytkownik musimy stworzyć użytkownika w linuksie o takiej samej nazwie jak użytkownik bazy

```
sudo adduser mkzetpl
```

Zalogowanie się i uruchomienie interfejsu jako użytkownik mkzetpl

```
sudo -u mkzetpl psql
```

Usunięcie użytkownika (role)

```
drop role mkzetpl;
```

Help do psql

```
psql --help
```

## Komendy PostgresSQL

Wyświetlenie role (użytkowników)

```
\du
```

Wyświetlenie wszystkich tabeli

```
\dt
```

Wyświetlenie istniejących baz danych

```
\l
```

Informacje z jakiego konta jesteśy zalogowani do postgres

```
\conninfo
```

Tworzenie role (użytkownika)

```
CREATE ROLE me WITH LOGIN PASSWORD 'password';
```

Dodanie uprawnień tworzenia bazy do role (użytkownika)

```
ALTER ROLE me CREATEDB;
```

Ustawiamy hasło do bazy

```
\password
```

Help - wyświetla komendy

```
\?
```

Połączenie do nowej bazy

```
\c nazwa_bazy
```

Wyjście z interfejsu postgres

```
\q
```

Tworzenie tabeli w bazie danych postgres

```
CREATE TABLE uzytkownicy (
   id_uzytkownika serial PRIMARY KEY,
   imie VARCHAR (50) NOT NULL,
   nazwisko VARCHAR (50) NOT NULL,
   wiek SMALLINT NOT NULL
);
```

Dodanie do tabeli

```
INSERT INTO uzytkownicy (imie,nazwisko,wiek)
VALUES ('Jan','Kowalski',50);
```

Wyświetlenie wszystkich tabel w bazie

```
\dt
```

Wyświetlenie zawartości całej tabeli

```
SELECT * FROM uzytkownicy;
```
