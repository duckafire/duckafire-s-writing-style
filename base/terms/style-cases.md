# Style cases

The goal of this document is to define the names and characteristics of most famous and used style cases — in programming context. they are writing styles used to name mainly identifiers.

(It is RECOMMENDED use only ASCII characters, or non-ASCII characters that have an *ASCII version*, to name identifiers.)

* `lcase`:
  * only lower case characters; and
  * different words, abbreviations, and acronyms MUST NOT be separated.

* `UCASE`:
  * only upper case characters; and
  * different words, abbreviations, and acronyms MUST NOT be separated.

* `snake_case`:
  * only lower case characters;
  * different words and acronyms MUST be separated with one underscore; and
  * only formal full words and formal acronyms.

* `MACRO_CASE`:
  * only upper case characters;
  * different words and acronyms MUST be separated with one underscore; and
  * only formal full words and formal acronyms.

* `css-case`:
  * only lower case characters;
  * different words and acronyms MUST be separated with one hyphen; and
  * only formal full words and formal acronyms.

* `COBOL-CASE`:
  * only upper case characters;
  * different words and acronyms MUST be separated with one hyphen; and
  * only formal full words and formal acronyms.

* `camelCase`:
  * all characters of the first word or acronym MUST be lower case;
  * first character, from second to last word or acronym, MUST be upper case, and all other ones MUST be lower case; and
  * only formal full words and formal acronyms.

* `PascalCase`:
  * first character of word or acronym, MUST be upper case, and all other one MUST be lower case; and
  * only formal full words and formal acronyms.

> `lcase`, `UCASE`: it is RECOMMENDED identifiers that use this style case being short and prioritizing abbreviation (even informal), because they can easily became hard to read.
>
> It is NOT RECOMMENDED to use informal abbreviation that are not commonly known and adopted.

> `camelCase`, `PascalCase`: only first character of acronyms is upper case (from second to last), instead of all them, because it can became hard to read identifiers that are formed by more than one acronym; like: `IsHTTPURL`.
