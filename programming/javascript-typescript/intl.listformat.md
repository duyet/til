---
description: Convert arrays to human-readable lists
---

# Intl.ListFormat



```javascript
const books = [
    'Harry Potter',
    'Bhagavad Gita',
    'The Alchemist',
    'Birthday Girl'
]

const listFormatter1 = new Intl.ListFormat('en', {
    style: 'long',
    type: 'conjunction'
})
console.log(listFormatter1.format(books));
// Harry Potter, Bhagavad Gita, The Alchemist, and Birthday Girl

const listFormatter2 = new Intl.ListFormat('en-GB', {
    style: 'short',
    type: 'disjunction'
})
console.log(listFormatter2.format(books));
// Harry Potter, Bhagavad Gita, The Alchemist, or Birthday Girl

```



The first part is to create the formatter using the `Intl.ListFormat` method. This method accepts two optional parameters.

* `locales` - A string with a BCP 47 language tag, or an array of such strings.
* `options` - An object with some or all of the following properties:
  * `localeMatcher` - The locale matching algorithm to use. Possible values are `lookup` and `best fit`; the default is `best fit`.
  * `type` - The format of the output message. Possible values are `conjunction` that stands for “and”-based lists (default, e.g., “A, B, and C”), or `disjunction` that stands for “or”-based lists (e.g., “A, B, or C”). `unit`stands for lists of values with units (e.g., “5 pounds, 12 ounces”).
  * `style` - The length of the formatted message. Possible values are: `long`(default, e.g., “A, B, and C”); `short` (e.g., “A, B, C”), or `narrow` (e.g., “A B C”). When style is `short` or `narrow`, `unit` is the only allowed value for the type option.

Source: [https://www.amitmerchant.com/how-to-convert-arrays-to-human-readable-lists-in-javascript/](https://www.amitmerchant.com/how-to-convert-arrays-to-human-readable-lists-in-javascript/)
