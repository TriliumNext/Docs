# Search
*   local search - searches within currently displayed note. Press `CTRL-F` to open the search dialog. In server version this is handled by the browser, in desktop (electron) version there's a separate dialog.
*   note search - you can find notes by search for text in the title, note's content or note's [attributes](Attributes.md). You can also [save search](Saved-search.md).
    *   You can activate note search by clicking on magnifier icon on the left or pressing `CTRL-S` keyboard [shortcut](Keyboard-shortcuts.md).

Simple note search examples
---------------------------

`rings tolkien` - fulltext search, this will try to find notes which have anywhere words "rings" and "tolkien"

`"The Lord of the Rings" Tolkien` - same as above, but "The Lord of the Rings" must be exact match

`note.content *=* rings OR note.content *=* tolkien` to find notes which contain "rings" or "tolkien"

`towers #book` - combination of fulltext search with attribute search - this looks for notes containing "towers" word anywhere, and they also need to have "book" label

`towers #book or #author` - searches notes containing "towers" word anywhere and matching note must have either "book" or "author" label

`towers #!book` - searches notes containing "towers" word anywhere and which do **not** have "book" label

`#book #publicationYear = 1954` - will find notes with "book" label and label "publicationYear" containing this specific value

`#genre *=* fan` - matches notes with "genre" label which has value which contains "fan" substring. Besides `*=*` for "contains", there's also `=*` for "starts with", `*=` for "ends with", `!=` for "is not equal to"

`#book #publicationYear >= 1950 #publicationYear < 1960` - you can also use numeric operators - this will find all books published in the 1950s

`#dateNote >= TODAY-30` - special "smart search" will find notes with label "dateNote" with date corresponding to last 30 days. Complete list of smart values: NOW +- seconds, TODAY +- days, MONTH +- months, YEAR +- years

`~author.title *=* Tolkien` - find notes which have relation "author" which points to a note with title containing word "Tolkien"

`#publicationYear %= '19[0-9]{2}'` - operator '%=' matches a regular expression (regex). Since Trilium 0.52

Advanced use cases
------------------

`~author.relations.son.title = 'Christopher Tolkien'` - This will search for notes which have “author” relation to a note which has a “son” relation to “Christopher Tolkien” note. This situation can be modeled by this note structure:

*   Books
    *   Lord of the Rings
        *   label: “book”
        *   relation: “author” points to “J. R. R. Tolkien” note
*   People
    *   J. R. R. Tolkien
        *   relation “son” points to "Christopher Tolkien" note
    *   Christopher Tolkien

`~author.title *= Tolkien OR (#publicationDate >= 1954 AND #publicationDate <= 1960)` - you can also use boolean expressions and parenthesis to group expressions

However, if your search expression starts with a parenthesis, it needs to be prepended by an "expression separator sign", either # or ~. So the equivalent expression, just reordered, would look like:

`# (#publicationDate >= 1954 AND #publicationDate <= 1960) OR ~author.title *= Tolkien`

`note.parents.title = 'Books'` will find all notes which have (at least one) parent note with name “Book”.

`note.parents.parents.title = 'Books'` This again works transitively, so this will find notes whose parent of parent is named ‘Book’.

`note.ancestors.title = 'Books'` This is sort of extension of parents - this will find notes which have an ancestor anywhere in their note path (so parent, grandparent, grand-grand-parent …) with title ‘Book’. This is a nice way how to reduce the scope of the search to a particular subtree.

`note.children.title = 'sub-note'` So this works in the other direction and will find notes which have (at least one) child called “sub-note”.

### Search with note properties

Note has certain properties which can be also used for searching:

*   `noteId`
*   `dateModified` - local dates are in the format "2019-05-19 16:39:47.003+0200"
*   `dateCreated`
*   `utcDateModified` - UTC dates are in the format "2019-05-19 14:39:47.003Z"
*   `utcDateCreated`
*   `isProtected` (true, false)
*   `type` (text, code, search, relation-map, book)
*   `title` (when you want to search specifically the title)
*   `text` - search through note title and content
*   `content` - search just through note content
*   `rawContent` - search through raw note content (HTML tags are kept). Since v0.46.
*   `ownedLabelCount`
*   `labelCount` (includes inherited labels)
*   `ownedRelationCount`
*   `relationCount` (includes inherited relations)
*   `ownedRelationCountIncludingLinks` and `relationCountIncludingLinks` - count also includes auto-generated relations `imageLink`, `internalLink`, `relationMapLink` and `includeNoteLink`
*   `ownedAttributeCount` = `ownedLabelCount` + `ownedRelationCount`
*   `attributeCount` = `labelCount` + `relationCount`
*   `targetRelationCount` - number of relations targeting this note
*   `targetRelationCountIncludingLinks` - count also includes auto-generated relations `imageLink`, `internalLink`, `relationMapLink` and `includeNoteLink`
*   `parentCount` - essentially number of [clones](Cloning%20notes.md)
*   `childrenCount`
*   `isArchived` (true, false)
*   `contentSize` - size of note content in bytes.
*   `noteSize` - estimated size of complete note (chiefly note content + note revision contents). Since v0.46.
*   `revisionCount` - number of note revisions.

These are accessed through `note.`, e.g.:

```text-plain
note.type = code AND note.mime = 'application/json'
```

### Order by and limit

```text-plain
#author=Tolkien orderBy #publicationDate desc, note.title limit 10
```

The example above will do the following things (in this sequence):

1.  find notes with label author having value “Tolkien”
2.  order the results by publicationDate in descending order (so the newest first)
3.  in case publication date is equal, use note.title as secondary ordering in ascending order (`asc` is the default and thus can be omitted)
4.  take only the first 10 results

### Negation

Some queries can be expressed only with negation:

```text-plain
#book AND not(note.ancestor.title = 'Tolkien')
```

This will find all the book notes which are not in the "Tolkien" subtree.

Under the hood
--------------

### Label and relation shortcuts

"Full" syntax for searching by labels is the following:

`note.labels.publicationYear = 1954` or `note.relations.author.title *=* Tolkien`

But given that searching by labels and relations is pretty common, there exists also a shortcut syntax:

`#publicationYear = 1954` or `#author.title *=* Tolkien` respectively.

### Separating fulltext and attribute parts

As you may have noticed from the examples above, search syntax allows seamlessly combining fulltext search with attribute-based search. How is this done?

Take `tolkien #book` as an example. It contains:

1.  fulltext tokens - `tolkien`
2.  attribute expressions - `#book`

The tricky part is to find out where does the fulltext end and where the attribute expression begins. This is done by detecting certain stop-characters/words - all tokens are considered as fulltext before one of `#`, `~` or `note.` prefixes are encountered. After that, all characters/tokens are understood as attribute expression.

If you want to use `#`, `~` or `note.` as part of fulltext, you need to escape them, see below for details.

There are certain corner cases where this is not sufficient, e.g:

```text-plain
tolkien (#publicationYear >= 1950 AND #publicationYear < 1960) OR #book`
```

Here the expression starts with `(` which isn't (intentionally) a stop-character, so the query above will not actually work as intended. Instead, in these corner cases we need to add a separate extra stop character - `#` or `~` so the fixed query should look like:

```text-plain
tolkien # (#publicationYear >= 1950 AND #publicationYear < 1960) OR #book`
```

The extra stop character has no other effect other than separating the fulltext part from the attribute expression part.

### Escaping special characters

Symbols or values sometimes have special meaning, which might be not what you intend. This can be fixed by either enclosing the strings containing special characters into quotes or escaping individual characters with backslash:

`"note.txt"` - "note." is normally stop-prefix, but here it will be used for fulltext search

`\#hash` - `#` is normally stop-character, but here it's escaped with backslash, so it's again used for fulltext

`#myLabel = 'Say "Hello World"'`

There are three supported types of quotes - single, double and backtick.

### Type coercion

It's important to realize that a label value is always technically a string, even if it contains logically different value. This then allows you to do things like:

```text-plain
note.dateCreated =* '2019-05'
```

This will find notes created in May 2019 by simply doing string "starts with" operation on the date.

This approach does not work well with numbers though, so whenever there is a numeric operator detected, the label values will be coerced from their normal string form into a numeric value for comparison. This then allows for e.g. `#publicationYear >= 1960` work correctly.

Auto trigger search from URL
----------------------------

Opening Trilium like in the example below will open the search pane and automatically trigger search for "abc":

```text-plain
http://localhost:8080/#?searchString=abc
```