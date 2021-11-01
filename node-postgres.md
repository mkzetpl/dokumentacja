# node-postgres

Instalacja node-postgres

```
npm i pg
```

users.js

```js
const express = require('express');
const app = express();
const port = 3001;
const db = require('./queries');

app.use(express.json());

app.use(
   express.urlencoded({
      extended: true,
   })
);

app.get('/users', db.getUsers);
app.get('/users/:id', db.getUserById);
app.post('/users', db.createUser);
app.put('/users/:id', db.updateUser);
app.delete('/users/:id', db.deleteUser);

app.listen(port, () => {
   console.log(`App running on port ${port}.`);
});
```

queries.js

```js
const Pool = require('pg').Pool;
const pool = new Pool({
   user: 'postgres',
   host: 'localhost',
   database: 'postgres',
   password: 'benio',
   port: 5432,
});

const getUsers = (request, response) => {
   pool.query('SELECT * FROM uzytkownicy', (error, results) => {
      if (error) {
         throw error;
      }
      response.status(200).json(results.rows);
   });
};

const getUserById = (request, response) => {
   const id = parseInt(request.params.id);

   pool.query(
      'SELECT * FROM uzytkownicy WHERE id_uzytkownika = $1',
      [id],
      (error, results) => {
         if (error) {
            throw error;
         }
         response.status(200).json(results.rows);
      }
   );
};

const createUser = (request, response) => {
   const { imie, nazwisko, wiek } = request.body;

   pool.query(
      'INSERT INTO uzytkownicy ( imie, nazwisko, wiek) VALUES ($1, $2, $3)',
      [imie, nazwisko, wiek],
      (error, results) => {
         if (error) {
            throw error;
         }
         response.status(201).send(`User added with ID:`);
      }
   );
};

const updateUser = (request, response) => {
   const id = parseInt(request.params.id);
   const { imie, nazwisko, wiek } = request.body;

   pool.query(
      'UPDATE uzytkownicy SET imie = $1, nazwisko = $2, wiek = $3 WHERE id_uzytkownika = $4',
      [imie, nazwisko, wiek, id],
      (error, results) => {
         if (error) {
            throw error;
         }
         response.status(200).send(`User modified with ID: ${id}`);
      }
   );
};

const deleteUser = (request, response) => {
   const id = parseInt(request.params.id);

   pool.query(
      'DELETE FROM uzytkownicy WHERE id_uzytkownika = $1',
      [id],
      (error, results) => {
         if (error) {
            throw error;
         }
         response.status(200).send(`User deleted with ID: ${id}`);
      }
   );
};

module.exports = {
   getUsers,
   getUserById,
   createUser,
   updateUser,
   deleteUser,
};
```

curl

```
POST:
curl --data "imie=Władysław&nazwisko=Łokietek&wiek=48" https://mkzet.pl/users

PUT:
curl -X PUT -d "imie=Władysław" -d "nazwisko=Jagiełło" -d "wiek=50" https://mkzet.pl/users/7

DELETE:
curl -X "DELETE" https://mkzet.pl/users/6
```
