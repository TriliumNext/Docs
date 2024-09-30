Document is [SQLite](https://www.sqlite.org) database which contains all notes, tree structure, metadata and most of the configuration.

## Location

Document is stored in the [data directory](data-directory.md).

## Demo document

When you run Trilium for the first time, it will generate a demo document for you as a starting point. It's also pretty useful for demonstration of some of Trilium's features, e.g.:

* [Relation map](relation-map.md)
* [Day notes](day-notes.md)
* [Weight tracker](weight-tracker.md)
* [Task manager](task-manager.md)
* [Custom CSS theme|Themes#custom-css-themes](themes.md) *Steel Blue*

### Restoring demo document

In some cases you might want to take a look at the demo document after you deleted it. Or you might want to see if there was something added (sometimes we add a new feature demonstration into demo document). In such case you can just [download .zip archive](https://github.com/TriliumNext/Notes/raw/master/db/demo.zip) of the latest document and import it somewhere into the tree (right-click on a note where you want to import the demo document and choose "Import").

## Manually modifying the document

Trilium provides a lot of flexibility, but with that you can also potentially shoot yourself in the foot (e.g. with startup script which blanks the app view).

In such cases you can manually fix notes on the database layer - you can use e.g. [https://sqlitebrowser.org/](https://sqlitebrowser.org/) to open `document.db` file, find problematic notes and manually fix them. Don't forget to commit / write changes after you're done.

## How to reset the document

If you previously just experimented with Trilium and want to get it to the initial state, you can do that by deleting the `document.db*` files, e.g. like this:

```bash
rm document.db*
```

If you don't need to preserve e.g. the `config.ini`, then you can also delete the whole [[data directory]] like this:

```bash
rm -r ./trilium-data
```

After starting next time, Trilium will create a new initial document.
