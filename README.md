# Gotchas

## React

__Error: event.persist__ - you're accessing the method currentTarget on a released/nullified synthetic event. Caused by React 16. Fixed in React 17

``` sh
npm i react@17 react-dom@17
```

## Git credentials

``` sh
git config --unset credential.helper 'cache'
git config --global --unset credential.helper 'cache'

git config --global --set credential.helper 'cache --timeout=10800'
```

## Heroku

Not a secure connection to pg so build fails
``` sh
heroku config:add PGSSLMODE=no-verify
```

## NPM

Unhandled rejection Error: Cannot find module '[stuff here]\binding\[blah blah]\node_sqlite3.node'
``` sh
npm install sqlite3 --build-from-source
```

????

``` sh
sudo apt install build-essential python
```

Unknown command: python - but they have python3
``` sh
sudo apt install python-is-python3
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
