# Floraverse Character Generator Data

The dataset used in the [Floraverse Character Generator](http://feuforeve.fr/FloraCharacterGenerator).
It is released under the Creative Commons BY-SA license.

The directory `images` contains various images from (or based on images from) the [Floraverse website](http://floraverse.com).

# Files
The files and their format is described below.

## calendar.json
Contains the description of the calendar year and astrological signs.

The root is an `object` containing two fields:
  - `months` (`list`: `month`): the list of months
  - `astrological-signs` (`list`: `sign`): the list of astrological signs

A `month` object has the following fields:
  - `number` (`integer`): the numerical representation of the month in dates
  - `name` (`string`): the name of the month
  - `days` (`integer`): the number of days in the month
  - `named-after` (`string`): the origin of the name

A `sign` object has the following fields:
  - `name` (`string`): the name of the sign
  - `symbol` (`string`): the path to the image of the symbol of the sign
  - `from` (`object`: `date`): the starting date of the astrological sign
  - `to` (`object`: `date`): the ending date of the astrological sign

A `date` objects used in the astrological signs has the folowing fields:
  - `month` (`integer`): the month of the date
  - `day` (`integer`): the day of the date

## genders.json
Contains the description of (english) genders. Mostly for grammatical use when generating sentences.

The root is a `list` of `gender` objects.

A `gender` object has the following fields:
  - `name` (`string`): the name of the gender
  - `title` (`string`): the honorific used to indicate the gender of a person
  - `title-abbreviation` (`string`): the abbreviation of the title
  - `subject-pronoun` (`string`): the 3rd person subject pronoun corresponding to the gender
  - `object-pronoun` (`string`): the 3rd person object pronoun corresponding to the gender
  - `genitive-adjective` (`string`): the 3rd person genitive adjective corresponding to the gender
  - `reflexive-pronoun` (`string`): the 3rd person reflexive pronoun corresponding to the gender
  - `plural?` (`boolean`): indicate if verbs should be conjugated in plural when the subject pronoun is the subject of a sentence

## sexes.json
Contains the description of biological sexes. Used when generating ancestors or descendants.

The root is a `list` of `sex` objects.

A `sex` object has the following fields:
  - `name` (`string`): the name of the sex
  - `context` (`string`): a description indicating in which context to use that object.
  - `mother?` (`boolean` or the `string` `"maybe"`): indicate if individuals of that sex are described as biological mother.
  - `gender-distribution` (`distribution`: `gender`): indicate the default distribution used when generating `gender` for individuals of the given `sex`.

A `distribution` of `gender` is described as a map object whose keys are the `name` of a given `gender` and associated values are `number` giving the corresponding weight in the distribution.

## elements.json
Contains the description of magical elements. Used for affinities.

The root is an `object` containing the following fields:
  - `none` (`element`): an element value used for a lack of elemental affinity
  - `primary` (`list`: `element`): the list of primary elements
  - `secondary` (`list`: `combined-element`): the list of secondary elements

The `element` object has the following fields:
  - `name` (`string`): the name of the element
  - `affinity-description` (`string`): a string used to describe someone or something having an elemental affinity
  - `related-nouns` (`list`: `string`): a list of nouns that can be used to convey the idea of the element
  - `related-adjectives` (`list`: `string`): a list of adjectives that can be used to convey the idea of the element

The `combined-element` object has the following fields:
  - `components` (`list`: `string`): a list of primary elements that compose a combined element; each string correspond to the name of a primary element
  - `result` (`element`): the resulting element of the combination

## mottos.json
Contains various mottos and a way to generate variations.

The root is an `object` containing the following fields:
  - `prefix` (`list`: `string`): a list of prefix for making variations of prefixable mottos.
  - `prefixable` (`list`: `string`): a list of prefixable mottos.
  - `unprefixable` (`list`: `string`): a list of unprefixable mottos.
