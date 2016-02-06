# Diacritic regex

Creates the inverse of transliterated string to a regex. What? Basically, a regex that is diacritic insensitive

## Why?

Sometimes the user will search for *blasé*, but your database is dumb and doesn't understand collations and diacritic insensitiveness, but it can compare stuff using regex, so there ya go.

## How?

Suppose you have the word *résumé* but written improperly in the database as *resume*. The user is clever, and types it correctly into the search box. Gets nothing. How to search for all the weird cases people mistype stuff when comes to accents?

```es6
import { toRegex } from 'diacritic-regex';

toRegex('résumé') // => /r[eéèêë]sum[eéèêë]/i;
toRegex('résumé', {flags: 'mu'}) // => /r[eéèêë]sum[eéèêë]/mu;
toRegex('résumé', {
  flags: '',
  mappings: {
    'é': ['e','é','É']
  }
}) // => /r[eéÉ]sum[eéÉ]/;
```

## License

MIT
