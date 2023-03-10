---
title: 'SyntaxError: JSON.parse: bad parsing'
slug: Web/JavaScript/Reference/Errors/JSON_bad_parse
tags:
  - Erreurs
  - JSON
  - JavaScript
  - NeedsExample
  - SyntaxError
translation_of: Web/JavaScript/Reference/Errors/JSON_bad_parse
original_slug: Web/JavaScript/Reference/Erreurs/JSON_bad_parse
---

{{jsSidebar("Errors")}}

## Message

```
SyntaxError: JSON.parse: unterminated string literal
SyntaxError: JSON.parse: bad control character in string literal
SyntaxError: JSON.parse: bad character in string literal
SyntaxError: JSON.parse: bad Unicode escape
SyntaxError: JSON.parse: bad escape character
SyntaxError: JSON.parse: unterminated string
SyntaxError: JSON.parse: no number after minus sign
SyntaxError: JSON.parse: unexpected non-digit
SyntaxError: JSON.parse: missing digits after decimal point
SyntaxError: JSON.parse: unterminated fractional number
SyntaxError: JSON.parse: missing digits after exponent indicator
SyntaxError: JSON.parse: missing digits after exponent sign
SyntaxError: JSON.parse: exponent part is missing a number
SyntaxError: JSON.parse: unexpected end of data
SyntaxError: JSON.parse: unexpected keyword
SyntaxError: JSON.parse: unexpected character
SyntaxError: JSON.parse: end of data while reading object contents
SyntaxError: JSON.parse: expected property name or '}'
SyntaxError: JSON.parse: end of data when ',' or ']' was expected
SyntaxError: JSON.parse: expected ',' or ']' after array element
SyntaxError: JSON.parse: end of data when property name was expected
SyntaxError: JSON.parse: expected double-quoted property name
SyntaxError: JSON.parse: end of data after property name when ':' was expected
SyntaxError: JSON.parse: expected ':' after property name in object
SyntaxError: JSON.parse: end of data after property value in object
SyntaxError: JSON.parse: expected ',' or '}' after property value in object
SyntaxError: JSON.parse: expected ',' or '}' after property-value pair in object literal
SyntaxError: JSON.parse: property names must be double-quoted strings
SyntaxError: JSON.parse: expected property name or '}'
SyntaxError: JSON.parse: unexpected character
SyntaxError: JSON.parse: unexpected non-whitespace character after JSON data
SyntaxError: JSON.parse Error: Invalid character at position {0} (Edge)
```

## Type d'erreur

{{jsxref("SyntaxError")}}

## Quel est le probl??me ?

Lorsque la m??thode {{jsxref("JSON.parse()")}} analyse (_parse_) une cha??ne de caract??res en JSON, cette cha??ne doit ??tre du JSON valide et une exception sera lev??e si la syntaxe est incorrecte.

## Exemples

### `JSON.parse()` n'accepte pas les virgules en fin de tableau

Les deux lignes qui suivent d??clencheront une exception `SyntaxError` :

```js example-bad
JSON.parse('[1, 2, 3, 4, ]');
JSON.parse('{"foo" : 1, }');
// SyntaxError JSON.parse: unexpected character
// at line 1 column 14 of the JSON data
```

Pour que la m??thode puisse analyser le JSON correctement, on ??vitera les virgules en fin de tableau :

```js example-good
JSON.parse('[1, 2, 3, 4 ]');
JSON.parse('{"foo" : 1 }');
```

### Les noms des propri??t??s doivent ??tre entre double quotes

On ne peut pas utiliser de quotes simples pour indiquer le nom d'une propri??t?? (ex. `'toto'`).

```js example-bad
JSON.parse("{'toto' : 1 }");
// SyntaxError: JSON.parse: expected property name or '}'
// at line 1 column 2 of the JSON data
```

?? la place, on ??crira `"toto"` :

```js example-good
JSON.parse('{"toto" : 1 }');
```

### Z??ros en d??but de nombres et points d??cimaux

On ne peut pas utiliser de z??ros en d??but de nombre (ex. 01). Par ailleurs, les nombres d??cimaux doivent avoir une partie d??cimale, on ne peut pas terminer un nombre par un point.

```js example-bad
JSON.parse('{"toto" : 01 }');
// SyntaxError: JSON.parse: expected ',' or '}' after property value
// in object at line 1 column 2 of the JSON data

JSON.parse('{"toto" : 1. }');
// SyntaxError: JSON.parse: unterminated fractional number
// at line 1 column 2 of the JSON data
```

Pour que cela fonctionne, on ??crira simplement 1 sans 0 devant et au moins un chiffre apr??s le s??parateur d??cimal :

```js example-good
JSON.parse('{"toto" : 1 }');
JSON.parse('{"toto" : 1.0 }');
```

## Voir aussi

- {{jsxref("JSON")}}
- {{jsxref("JSON.parse()")}}
- {{jsxref("JSON.stringify()")}}
