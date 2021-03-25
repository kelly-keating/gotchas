# Gotchas

## React

__Error: event.persist__ - you're accessing the method currentTarget on a released/nullified synthetic event. Caused by React 16. Fixed in React 17

``` sh
npm i react@17 react-dom@17
```
cannot find module 'fs'

- check for auto imports from the backend (e.g. request from express)

## Git credentials

``` sh
sudo git config --system --unset credential.helper

git config --global --set credential.helper 'cache --timeout=10800' // <-- this may be wrong?
```

## Heroku

Complains about `no pg_hba.conf ... SSL off` aka not a secure connection to pg so build fails
```sh
heroku config:add PGSSLMODE=no-verify
```

## NPM - sqlite3

Unknown command: python - but they have python3
``` sh
sudo apt install python-is-python3
```
Unhandled rejection Error: Cannot find module '[stuff here]\binding\[blah blah]\node_sqlite3.node'
``` sh
npm install sqlite3 --build-from-source
```
__make not found__ error
```sh 
sudo apt-get install build-essential python
```
if that fails to fetch, run this update command and then try again
```sh
sudo apt-get update
```
they may then get a __'python not found'__ error if the first command failed
```sh
sudo apt-get install python
npm i sqlite3
```

## Many to many

``` js
function getsoupsAndIngredientsNestedJoin(db = database) {
  return db('soups').select()
  .then(soups => {
    return Promise.all(soups.map(soup => {
      return db('ingredients')
      .join('soup_ingredients', 'soup_ingredients.ingredient_id', 'ingredients.id')
      .where('soup_ingredients.soup_id', soup.id)
      .select('ingredients.*')
      .then(ingredients => {
        soup.ingredients = ingredients
        return soup
      })
    }))
  })
  .then(soups => {
    return soups
  })
}
```
