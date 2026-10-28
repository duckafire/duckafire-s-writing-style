# Markdown

The goal of this document is record and explain the decisions behind of the writing style of Markdown used by [DuckAfire][]; it aims:

*   ensuring that the message stored in the document can be easily read by humans from the reading of document's source code in plan text — so that reading and understanding can be possible even if rendering is not —;

*   ensuring that screen readers can navigate through documents easily and that their users can understand the documents' content in a successful way; and

*   ensuring that the overwhelming majority of the Markdown parsers generate an equivalent HTML code — as way to avoid rendering problems that may make difficult to read and understand the document's content.

> The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all capitals, as shown here.

## Restrictions

### Inheritance from HTML

**Only standard elements from [Gruber's Markdown][] MUST be used.**

[John Gruber][] is the creator of Markdown; his documentation and processing script were the base to the most popular Markdown parsers. This fact makes it the best choose to ensure that most Markdown parsers can generate equivalent HTML codes and the expected rendering result.

> All terms used to refer Markdown elements are from official documentation of [Gruber's Markdown][].

---

**HTML tags and entities SHOULD NOT be used, except empty comment tags (`<!---->`), `&amp;`, `&lt;`, and `&quot;`.**

> Non-empty comment tags MUST NOT be used.

<!---->

> If Markdown elements are not sufficient, Markdown is not the best choose.

Introducing them in the source code may make it hard to read and understand.

Empty comment tags are allowed because they are a strong hack to ensure the separation between elements without affect rendering with a visually unnecessary element (like an horizontal line). It is useful mainly to separate lists — in same level —, block quotes, and code blocks. See example below:

    *   list one
    *   top level

        *   list one
        *   sub level

        <!---->

        *   list two

        *   sub level

    *   continuation of list one

    <!---->

    *   list two
    *   top level

    > Block quotes one

    <!---->

    > Block quotes two

        Code block one

    <!---->

        Code block two

(It works because Markdown parsers always preserve HTML tags — even when they are empty.)

The exceptions to `&amp;` and `&lt;` exist because [Gruber's Markdown][] does not ensure that ampersand character and less-than sign always will be automatically escaped when they are outside of a code span or code block; besides it, it does not provide a way to escape them through of the use of a backslash.

As for `&quot;`, it is allowed because [Gruber's Markdown][] does not provide other way to escape double quotes contained in title attributes — from link labels — delimited with double quotes.

### No reason to use

**Sharps MUST NOT be used after the text content of headings.**

Because there is no a really worth reason to do it. (And because it may be ugly if the text content is long.)

---

**Horizontal rule MUST be formed only with three characters.**

([Gruber's Markdown][] allows that horizontal rules have an unlimited length.)

Because there is no a really worth reason to write long horizontal rules. (The minimum is sufficient.)

---

**Hypertext references MUST NOT refer elements identifiers (`id`).**

Because [Gruber's Markdown][] is unable to define an `id` to an element.

### Element variants

**Tabulation character MUST NOT be used.**

Because some Markdown parsers may confuse code blocks with indentation — and vice versa — if they use tabulations.

---

**Underline MUST NOT be used to mark emphasis spans.**

Because underline may not be used in any context to mark emphasis span — because Markdown parsers may treat it as a word character —, unlike asterisk that can be used in any place.

---

**Asterisk and underline MUST NOT be used to mark horizontal rules.**

Because some Markdown parsers may confuse them with a emphasis span marking.

---

**Plus and hyphen MUST NOT be used to mark unordered list items; only asterisk MUST be.**

Because asterisks are more similar to a [bullet character][] that is commonly used as prefix to list items.

---

**Heading style inherited from [Setext][] MUST NOT be used.**

> This style may be watched below:
>
>     Heading level one
>     ===
>
>     Heading level two
>     ---
>
> (Quantity of equals sign and hyphens is unlimited.)

Because there is no a version to all heading levels and they occupy many lines.

### Delimiters

**Only double quotes MUST be used to delimit the title attribute link labels.**

Because it is arguably less used than apostrophes (single quotes) and parentheses in titles.

> If, for some reason, a double quotes characters is "required" in a title attribute, the entity name (from [HTML entities][]) `&quot;` MUST be used to represent it.

---

**Hypertext references of link labels MUST NOT be delimited with angle brackets.**

Because this document already defines rules that, when correctly followed, ensure that hypertext references will be treat as expected — in all contexts where they may be used.

## Syntax precautions

### Escaping characters

**[URL Encoding][] MUST be used to represent closing parenthesis, single quotes, double quotes, greater-than sign, and space character that are part of hypertext references contained in link labels or automatic links.**

Because these elements use these characters in their syntax, which may confuse some Markdown parsers. (Always using the [URL Encoding][] ensures the cited characters always will be treated as part of the hypertext references.)

> This rules was designed to standardize the writing of hypertext references — in all scenarios where they may be used to refer something.

The respective [URL Encoding][] codes are listed below:

*   Closing parenthesis (`)`): `%29`.

*   Single quotes (`'`): `%27`.

*   Double quotes (`"`): `%22`.

*   Greater-than sign (`>`): `%3E`.

*   Space character (` `): `%20`.

---

**The literal ampersand character and less-than sign always SHOULD be represented by their respective entity names, from [HTML entities][], except when they are in a code span and code block.**

> Do not confuse entity names (`&quot;`) with entity numbers (`&#34;`).
>
> (Entity numbers MUST NOT be used because they are harder to remember than entity names.)

It ensures that most Markdown parsers always will treat them as characters, because [Gruber's Markdown][] only ensures they will be automatically escaped when they are in a code span or code block.

The respective [HTML entities][] are listed below:

*   Ampersand (`&`): `&amp;`.

*   Less-than sign (`<`): `&lt;`.

---

**The literal double quotes MUST be represented by its respective entity name, from [HTML entities][], when it is contained in a title attribute — of a link labels — delimited with double quotes.**

Because [Gruber's Markdown][] does not provide other way to escape it.

The respective [HTML entities][] is below:

*   Double quotes (`"`): `&quot;`.

---

**The literal backslash, crasis, asterisk, underline, sharps, opening square bracket, both curly brackets, plus, and minus always MUST be escaped — with a backslash as prefix — when they are not used as marking to something and are not in a code span or code block.**

It ensures that most Markdown parsers always will treat them as characters when it is desired. Some of them may be automatically escaped, but scenarios are uncertain.

(Frequency of use was also used as criterion to choose them.)

> Parentheses, closing square brackets, and exclamation sign never need to be escaped because opening square brackets always will be escaped.

---

**The literal character dot SHOULD be escaped when it is the first graphic character after an integer number that starts a line, except when they are in a code span or code block.**

It ensures that most Markdown parsers always will treat it as a character, without cluttering texts with many redundant backslashes — because it is much common in writing.

> See this example of scenario:
>
>     *   Lorem ipsum odor amet, consectetuer adipiscing elit:
>         2000\.

### While-spaces

**One empty line SHOULD be placed before and after each element, except between list items from a same list — of any type — formed only with list items that contain only one primitive word, compound word, acronym of any type, or any type of noun.**

> The exception exists because lists with single words is easier to read when their items are close; unlike lists with (long) phrases.

<!---->

> In case of doubt about lists, see this example of code:
>
>     *   one
>     *   two
>     *   three
>
>     ---
>
>     *   one long
>
>     *   two long
>
>     *   three long
>
> (It MUST be applied to any type of list. First list is the exception of the rule addressed here; second is not.)

This measure has as goal to avoid that most Markdown parsers confuse different elements, which — due to way [Gruber's Markdown][] was designed — may occur often; like example below:

    Lorem ipsum ...
        int foo = 0;

(Where some Markdown parsers may treat the snippet as just one paragraph, instead to treat it as one paragraph and one code block.)

---

**Line breaks MUST NOT be used to limit length of paragraphs' lines.**

> It **is not** refer to line break mark (trailing spaces) — that generates a `<br/>`.

Because most code editors and IDEs are unable to break lines of a text line — respecting words and punctuations — when a specific length is reached and to update length of lines when the length of a previous lines is changed.

Even that doing it manually is simple, it may make rendering in plan text uncomfortable in screens or windows which width is smaller than lines' length; in addition to make changelogs of versioning patches more long.

> Line breaks still may be and should be used to improve source code organization and legibility, like below:
>
>     *   Lorem ipsum odor amet:
>         consectetuer adipiscing elit.
>
>     *   Potenti ultricies inceptos:
>         quam facilisis aliquam vehicula quis.
>
>     *   Laoreet proin magna inceptos senectus lorem:
>         Penatibus etiam metus quam sodales nisi.

---

**One — and only one — space character MUST be placed: after less-than sign used to mark a non-empty line of a block quotes; after the last sharp of a chain used to mark a heading of any level; and between the identifier and the hypertext reference of a link label.**

It ensures that most Markdown parsers can identify and treat these marking as expected (without to confuse them with regular characters).

---

**Three space characters MUST be placed after the character used to mark an item of an unordered list — between element's marking and its text content.**

Because it allows that all their child elements may be correctly nested — using indentation.

---

**Two space characters MUST be placed after the characters used to mark an item of an ordered list — between element's marking and its text content.**

Because it allows that all their child elements may be correctly nested — using indentation.

---

**All child elements from list items, from second, MUST be indented one level (four space characters) above the indentation of their parent.**

It ensures that most Markdown parsers nest them correctly and it improves source code legibility.

> In case of doubt about lists, see this example of code:
>
>     *   Lorem ipsum odor amet.
> 
>         Consectetuer adipiscing elit.
>
>         Potenti ultricies inceptos
> 
>         Quam facilisis aliquam vehicula quis.

---

**Trailing spaces MUST NOT be used to create HTML's tag of line break.**

Because most code editors and IDEs are unable to render them graphically, making them hard to locale, which can cause some rendering bugs.

(They are also not visible in plan text, but it does not affect the reading or something related with it.)

---

**White-space characters MUST NOT be placed after of the opening delimiters and before of the closing delimiters of emphasis spans, reference links, identifier of link labels, automatic links, and reference images.**

It ensures different Markdown parsers can identify and treat them as expected.

---

**Space characters MUST NOT be placed between the parts — delimited with square brackets; and delimited with parentheses or square brackets — of reference links and reference images.**

It ensures that most Markdown parsers can identify and treat them as expected; furthermore strengthen visually the relation between the parts — helping to improve source code legibility.

## Elements nesting

**Italic-bold emphasis spans MUST NOT nest other emphasis spans.**

Because there is no a really worth reason to do it.

---

**Reference links MAY contain only emphasis spans, code spans, reference links, automatic links, and allowed HTML entities, but it is NOT RECOMMENDED.**

These elements had chosen because only they are inline; in other words, only they may be included between snippets of text without break their flow — they are treated as part of the text; of the flow.

It is NOT RECOMMENDED because most Markdown parsers resolve reference links before resolve the marking inside of them, that is, all that is contained in the square brackets — including valid marking characters — will be used to assemble the identifier that will be used to search for a match link label (with identifier is equal) before to expand the elements — **if** it expands —, which disrupts the use of *implicit link names*.

> Emphasis spans still may be placed around them, like: `**[foo][]**`. But code spans may not be: ``[`foo`][]``.

---

**Headings of any level and paragraphs MAY contain only emphasis spans, code spans, reference links, automatic links, and allowed HTML entities.**

Because only these elements are inline; in other words, only they may be included between snippets of text without break their flow — they are treated as part of the text; of the flow.

> Some headings styles, from some Markdown parsers, may hide graphically the presence of emphasis spans included in headings (during rendering).

---

**List items of any type of list MUST NOT nest headings of any level; all other allowed elements MAY be nested in them.**

> All their child elements MUST be indented with four space characters above the indentation of they parents.

Because it may break the headings hierarchy.

---

**Block quotes MUST NOT nest headings of any level or block quotes; all other allowed elements MAY be nested in them.**

Because it may break the headings hierarchy; and because there is no a really worth reason to nest block quotes in block quotes — it may make things confuse.

## Code legibility

### Organization

**Items' indexes from ordered lists MUST be manually ordered — from number one to their last number/index.**

Because it ensures that source code readers can understand easily the ordering of ordered lists — mainly of **long** lists.

> This may make boring or slow to add/remove items from ordered lists, but it still can help source code readers.

---

**Heading MUST be ordered based in their hierarchy — like it occurs with HTML.**

> Summary of heading hierarchy:
>
> *   heading level one defines document's subject;
>
> *   headings level two divide document's subject in long sections;
>
> *   level tree divide levels two in subsections;
>
> *   and level four, five, and six do the same to their respective parent headings.
>
> The level of a heading MUST be equal to the level of the last heading previous to it, that level minus one, or that level plus one; if there is not heading before it, its level MUST be one (because it is the first heading of the document).

Because it improves the legibility of the document (in plain text and rendered text) and the accessibility of the rendered text — to screen readers.

---

**The title attribute of link labels always MUST be placed in the following line after the start of their marking, with four space characters of indentation.**

> In case of doubt about it, see this example of code:
>
>     [foo]: https://example.com/
>         "Example company"
>
>     [bar]: https://example.org/
>         "Example organization"

Because it allows to align vertically the title attribute of all link labels, which improves source code legibility — mainly if the hypertext reference is long.

### Clear content

**Local file paths MUST start with `./`.**

(Local file paths are part of the group of hypertext references.)

It ensures that local documents may be easily found by source code readers.

---

**Each document MUST have one, and only one, heading level one.**

Because it is necessary to ensure that headings hierarchy is followed — like it occurs with HTML. (It defines that heading level ones MUST declare the main subject of a document.)

---

**Heading level one MUST be the first element of a document — placed in its first line.**

Because it is responsible to announce the documents' subject, therefore document top is the best position to it.

---

**Inline links and inline images MUST NOT be used; only reference links and reference images MUST be.**

> (Reference links and reference images require of a link labels.

It improves source code legibility, because it reduces the length of the marking required to define a link or an image; in addition to it, it allows to use *implicit link name* shortcut in reference links, which may reduce even further the length of them.

> See these examples:
>
>     Lorem ipsum [odor amet](https://example.com/user/e1527794ad12e5584986edaeb21a97e9264a34e95d107597c311a79c4b84a9dd462916c018113ac6138fc732a8a7caf571085d51725b17d66dc6ef4d3ab51f05 "odor amet"), consectetuer adipiscing elit. Potenti ultricies inceptos, quam facilisis aliquam vehicula quis. Laoreet proin magna inceptos senectus lorem.
>
> <!---->
>
>     Lorem ipsum [odor amet][], consectetuer adipiscing elit. Potenti ultricies inceptos, quam facilisis aliquam vehicula quis. Laoreet proin magna inceptos senectus lorem.
>
>     [odor amet]: https://example.com/user/e1527794ad12e5584986edaeb21a97e9264a34e95d107597c311a79c4b84a9dd462916c018113ac6138fc732a8a7caf571085d51725b17d66dc6ef4d3ab51f05  
>         "odor amet"

---

**Even that possible, the identifier of a link label SHOULD be equal to the text that will contain its hypertext reference; if it is not possible, a meaningful name MUST be given to it.**

> Since these identifiers are case insensitive, it is RECOMMENDED that the alphabetic characters present in them always use lower case.

It allows that *implicit link name* shortcut may be used to refer link labels, which makes source code cleaner. (Besides of allowing document maintainers written less.)

> In case of doubt about it, see this example of code:
>
>     [Lorem ipsum][] odor amet, consectetuer adipiscing elit.
>     Potenti ultricies inceptos, quam facilisis aliquam vehicula quis.
>     Laoreet proin magna inceptos senectus lorem.
>
>     [lorem ipsum]: https://en.wikipedia.org/wiki/Lorem_ipsum
>         "Wikipedia: Lorem ipsum"

### Accessibility

**Reference images SHOULD NOT be used.**

Because there is no a satisfactory way to render images in plan text, so it may be hard to understand them from reading of document's source code or through the use of a screen reader — even with a good alternative text.

Therefore, only use images when they are strictly required and may be transcribed with an alternative text — which, in itself, makes an image unnecessary.

---

**All references images MUST have a transcription — an alternative text.**

So that source code readers and screen reader users (with visual impairment) can understand images' content.

---

**Links labels MUST have a title attribute which content is related with their hypertext reference.**

For links, it is important to give to readers a tip about the destine of links' hypertext references, mainly when they are ambiguous, hard to understand, or abstract — like `https://example.com/2c26b`.

For images, it is important to attach extra information on it, as way to facilitate the interpretation of their visual content — since [Gruber's Markdown][] does not make available a way to add captions to an image (paragraphs are not captions).

[duckafire]: https://duckafire.gitlab.io/pages/home
    "DuckAfire's Nest"

[gruber's markdown]: https://daringfireball.net/projects/markdown/syntax
    "Daring Fireball: Markdown"

[john gruber]: https://en.wikipedia.org/wiki/John_Gruber
    "Wikipedia: John Gruber"

[html entities]: https://www.w3schools.com/html/html_entities.asp
    "W3 Schools: HTML entities"

[bullet character]: https://en.wikipedia.org/wiki/Bullet_(typography)
    "Wikipedia: bullet character (typography)"

[setext]: https://en.wikipedia.org/wiki/Setext
    "Wikipedia: Setext"

[url encoding]: https://www.w3schools.com/tags//ref_urlencode.asp
    "W3 Schools: URL Encoding (Percent Encoding)"
