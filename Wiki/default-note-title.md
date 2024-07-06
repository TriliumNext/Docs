# Default-note-title
When a new note is created, its name is by default "new note". In some cases, it can be desirable to have a different or even a dynamic default note title.

For this use case, Trilium (since v0.52) supports `#titleTemplate` [label](attributes.md). You can create such a label for a given note, assign it a value, and this value will be used as a default title when creating child notes. As with other labels, you can make it inheritable to apply recursively, and you can even place it on the root note to have it applied globally everywhere.

As an example use case, imagine you collect books you've read in a given year like this:

*   2022 Books
    *   Neal Stephenson: Anathem, 2008
    *   Franz Kafka: Die Verwandlung, 1915

Now, to the parent note "2022 Books" you can assign label `#titleTemplate="[Author name]: [Book title], [Publication year]"`.

And all children of "2022 Books" will be created with initial title "\[Author name\]: \[Book title\], \[Publication year\]". There's no artificial intelligence here, the idea is to just prompt you to manually fill in the pieces of information into the note title by yourself.

Dynamic value
-------------

The value of `#titleTemplate` is evaluated at the point of note's creation as a JavaScript string, which means it can be enriched with the help of JS string interpolation with dynamic data.

As an example, imagine you collect server outage incidents and write some notes. It looks like this:

*   Incidents
    *   2022-05-09: System crash
    *   2022-05-15: Backup delay

You can automatize the date assignment by assigning a label `#titleTemplate="${now.format('YYYY-MM-DD')}: "` to the parent note "Incidents". Whenever a new child note is created, the title template is evaluated with the injected [now](https://day.js.org/docs/en/display/format) object.

Second variable injected is [parentNote](https://zadam.github.io/trilium/backend_api/Note.html), an example could be `#titleTemplate="${parentNote.getLabelValue('authorName')}'s literary works"`.

See also \[\[[template](template.md)\]\] which provides similar capabilities, including default note's content.
