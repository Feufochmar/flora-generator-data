# Floraverse Character Generator Data

The dataset used in the [Floraverse Character Generator](http://feuforeve.fr/FloraCharacterGenerator).
It is released under the Creative Commons BY-SA license.

The directory `images` contains various images from (or based on images from) the [Floraverse website](http://floraverse.com).

# Files
The files and their format is described below.

## calendar.json
Contains the description of the calendar year and astrological signs.

The root object contains two fields:
  - `months` (`list`: `month`): the list of months
  - `astrological-signs` (`list`: `sign`): the list of astrological signs

A `month` object has the following fields:
  - `number` (`integer`): the numerical representation of the month in dates
  - `name` (`string`): the name of the month
  - `days` (`integer`): the number of days in the month

A `sign` object has the following fields:
    - `name` (`string`): the name of the sign
    - `symbol` (`string`): the path to the image of the symbol of the sign
    - `from` (`object`: `date`): the starting date of the astrological sign
    - `to` (`object`: `date`): the ending date of the astrological sign

A `date` objects used in the astrological signs has the folowing fields:
  - `month` (`integer`): the month of the date
  - `day` (`integer`): the day of the date
