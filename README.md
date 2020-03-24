# Floraverse Character Generator Data

The dataset used in the [Floraverse Character Generator](http://feuforeve.fr/FloraCharacterGenerator).
It is released under the Creative Commons BY-SA license.

The directory `images` contains various images from (or based on images from) the [Floraverse website](http://floraverse.com).

The input files used for generating names are not present in this repository.
They use [Phonagen](http://feuforeve.fr/Phonagen), and the languages used by the character generator are present as examples in the Phonagen repository.

# Files
The files and their format is described below.

For the `json` files, the type of the root is given.
When describing a field, the key of the field is followed by the expected type of the field in parentheses.
A `distribution` of type `type` is a map object whose keys correspond to the value of the `name` field of the given `type` and associated values are `number` giving the corresponding weight in the distribution.

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
  - `from` (`date`): the starting date of the astrological sign
  - `to` (`date`): the ending date of the astrological sign

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
  - `subject` (`string`): the 3rd person subject pronoun corresponding to the gender
  - `object` (`string`): the 3rd person object pronoun corresponding to the gender
  - `genitive` (`string`): the 3rd person genitive adjective corresponding to the gender
  - `reflexive` (`string`): the 3rd person reflexive pronoun corresponding to the gender
  - `plural?` (`boolean`): indicate if verbs should be conjugated in plural when the subject pronoun is the subject of a sentence

## sexes.json
Contains the description of biological sexes. Used when generating ancestors or descendants.

The root is a `list` of `sex` objects.

A `sex` object has the following fields:
  - `name` (`string`): the name of the sex
  - `context` (`string`): a description indicating in which context to use that object.
  - `mother?` (`boolean` or the `string` `"maybe"`): indicate if individuals of that sex are described as biological mother.
  - `gender-distribution` (`distribution`: `gender`): indicate the default distribution used when generating `gender` for individuals of the given `sex`.

## elements.json
Contains the description of magical elements. Used for affinities.

The root is an `object` containing the following fields:
  - `none` (`element`): an element value used for a lack of elemental affinity
  - `primary` (`list`: `element`): the list of primary elements
  - `secondary` (`list`: `combined-element`): the list of secondary elements
  - `tertiary` (`list`: `combined-element`): the list of tertiary elements usable by the generator. The composition may diverge from what is described in the comic.
  - `tertiary-exact` (`list`: `combined-element`): the list of tertiary elements as described in the Floraverse comic, but not usable by the generator

The `element` object has the following fields:
  - `name` (`string`): the name of the element
  - `affinity-description` (`string`): a string used to describe someone or something having an elemental affinity
  - `related-nouns` (`list`: `string`): a list of nouns that can be used to convey the idea of the element
  - `related-adjectives` (`list`: `string`): a list of adjectives that can be used to convey the idea of the element

The `combined-element` object has the following fields:
  - `components` (`list`: `string`): a list of elements that compose a combined element; each string correspond to the name of an element.
  - `result` (`element`): the resulting element of the combination

## mottos.json
Contains various mottos and a way to generate variations.

The root is an `object` containing the following fields:
  - `prefix` (`list`: `string`): a list of prefix for making variations of prefixable mottos.
  - `prefixable` (`list`: `string`): a list of prefixable mottos.
  - `unprefixable` (`list`: `string`): a list of unprefixable mottos.

## geography.json
Contains the locations. Those are described in a tree structure with places containing other places.

The root is an `object` containing the following fields:
  - `location-types` (`list`: `location-type`): the list of location types
  - `places` (`place`): the root location (the world)

The `location-type` object contains the following fields:
  - `name` (`string`): the name of location type
  - `preposition-in` (`string`): the preposition to use when indicating something is inside a location of that type
  - `preposition-near` (`string`): the preposition to use when indicating something is near a location of that type

The `place` object contains the following fields:
  - `name` (`string`): the name of the location
  - `reference-link` (`string`, optional): an URL to the page where the location is described. If a location has no `reference-link`, it means that it is the same as the parent location.
  - `type` (`string`): the name of a `location-type` indicating the type of the place
  - `restricted?` (`boolean`, optional): if `true`, indicate a location (and its sub-locations) cannot be freely used in generated contents. Default to `false`.
  - `locations` (`list`: `place`, optional): a list of places located inside the place. Empty by default.

## species.json
Contains the species.

The root is an `object` containing the following fields:
  - `defaults` (`species`): the default values of the species structure. These values are used when not explicited in a species of the list of species.
  - `species` (`list`: `species`): the list of species.
  - `crossbreeds` (`list`: `crossbreed`): the list of crossbreed species. Only childs whose parents are of different species are described.

The `species` object contains the following fields:
  - `name` (`string`): the name of the species
  - `reference-link` (`string`): an URL to the page where the species is described.
  - `endemic-in` (`list`: `string`): a list of `place` names where the species is usually found.
  - `restricted-to-endemic-areas?` (`boolean`): if `true`, indicate the species can only be found in the places where it is endemic.
  - `affinity` (`distribution`: `element`): the distribution of elemental affinity of the species
  - `sex` (`distribution`: `sex`): the distribution of sexes of the species
  - `reproduction` (`string`): the way the species reproduce. Possible values are:
    - `sexual` for sexual reproduction
    - `asexual` for asexual reproduction
    - `artifact` for species whose member are built rather than born
  - `asexual-parent-species` (`list`: `string`): a list of `species` `name` used in asexual reproduction to indicate which species can generate a member of this species
  - `generable-as-character?` (`boolean`): if `true`, the species can be used by the character generator to generate a character
  - `citizen?` (`boolean`): if `true`, indicate that member of this species would be considered citizen in civilized places. Usually means that members of this species have a rather high level of intelligence.
  - `pet?` (`boolean`): if `true`, indicate that member of this species could be raised as pets or domestic animals in civilized places.
  - `wild?` (`boolean`): if `true`, indicate that member of this species are usually considered as wild animals in civilized places.
  - `vegetal?` (`boolean`): if `true`, indicate a species whose members are unable to move on their own, like trees.
  - `mimic?` (`boolean`): if `true`, indicate the species physically mimics other species, and member of this species (the real species) must be instanciated with another associated species (the immited species). Members of this species usually physically look like members of the immited species, but with modifications from their real species.
  - `mimic-method` (`mimic-filter`): indicate the filter used for a mimic species to choose the assoicated species during instanciation.
  - `mimic-genes-used?` (`boolean`): if `true`, indicate the genes used to compute the species use the real species. If `false`, the genes use the immited species.
  - `varieties` (`list`: `species`): a list of species based on this species. They used the values of this species as default values and can be considered as variations of a same species.

The `mimic-filter` object contains the following fields:
  - `species` (`species`): a filter on the species fields. The associated value may be the value to search or an object of the form `{"not": [...]}` to list the values to exclude.
  - `relationship` (`string`, optional): a filter indicating a relationship between the character of the mimic species and another character from which the species is copied.

The `crossbreed` object contains the following fields:
  - `parents` (`list`: `string`): a list of parent species that give birth to a crossbreed; each string correspond to the name of an species.
  - `child` (`species`): the crossbreed species; only fields that should be forced instead of computed are needed. An empty object indicate crossbreed is possible.

## word-lists.json, natures.json
Contains dictionaries of words classified by categories.
  * `natures.json` is specific to personnality traits.
  * `word-lists.json` contain generic categories used for generating various character traits.

The root is an `object` whose fields indicate the name of the category and associated values are `list` of `string` containing the different words of the category.

## traits.json
Contains lists of templated sentences grouped in categories.

The root is an `object` whose fields indicate the name of the category and associated values are `list` of `sentence`.

A `sentence` is a list of tokens which can be either a `string` or a `token`.
The sentence is generated by replacing the tokens by strings and concatenating the resulting string list with spaces.
A sentence often need a `gender` instance as input to generation (as defined in `genders.json`).

A `token` is a `object` containing a single field among those:
  - `gender` (`string`): the token should be replaced by the indicated field of a `gender` instance.
  - `verb` (`string` or `token`): the token should be replaced by a conjugated form of the value using the `plural?` field of a `gender` instance.
  - `undefined-article` (`string` or `token`): the token should be replaced by the value prefixed by the undefined article and a space.
  - `plural` (`string` or `token`): the token should be replaced by the plural form of the value.
  - `word` (`string`): the token should be replaced by one of the word of the indicated category (from `word-lists.json`).
  - `species` (`string`): the token should be replaced by the `name` field of one of the `species` instance (from `species.json`) whose field indicated by the value is set to `true`.
  - `nature` (value unused): the token should be replaced by a word from a category of `natures.json`. The value is unused and should be set to `true`.
  - `location` (value unused): the token should be replaced by the `name` field of a `location` instance (from `geography.json`). The value is unused and should be set to `true`.

Some fields can take a `token` object as a value. Those should be replaced by a `string` before applying the token rule.

## abilities.json
Contains the list of abilities.

The `root` is a `list` of `ability` objects.

An `ability` object contains the following fields:
  - `name` (`string`): the name of the ability
  - `description` (`string`): the description of the ability
  - `author` (`string`): the original author behind the ability
  - `conditions` (`list`: `ability-condition`): a list of conditions to get the ability. A generated character can get the ability if one of the condition is respected.

An `ability-condition` object contains the following fields:
  - `type` (`string`): indicate the kind of condition. The possible values are the strings `"species"` and `"affinity"`.
  - `automatic?` (`boolean`): indicate if the ability is automatically got when the condition is respected

A species condition contains the following fields:
  - `species` (`string` or `list`: `string`): The species or list of species a character should have in its genes to get the ability.
  - `gene-threshold` (`number`): the percentage of genes of the species to get the ability

An affinity condition contains the following fields:
  - `affinity` (`string`): the needed affinity to get the ability
