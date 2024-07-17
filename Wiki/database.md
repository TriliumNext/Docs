# Database
Your Trilium data is stored in a [SQLite](https://www.sqlite.org) database which contains all notes, tree structure, metadata, and most of the configuration. The database file is named `document.db` and is stored in the application's default [data directory](data-directory.md).

## Demo Notes

When you run Trilium for the first time, it will generate a new database containing demo notes. These notes showcase its many features, such as:

*   [Relation Map](relation-map.md)
*   [Day Notes](day-notes.md)
*   [Weight Tracker](weight-tracker.md)
*   [Task Manager](task-manager.md)
*   [Custom CSS Themes](themes.md)

### Restoring Demo Notes

There are some cases in which you may want to restore the original demo notes. For example, if you experimented with some of the more advanced features and want to see the original reference, or if you simply want to explore the latest version of the demo notes, which might showcase new features.

You can easily restore the demo notes by using Trilium's built-in import feature by importing them:
- Download [this .zip archive](https://github.com/TriliumNext/Notes/raw/stable/db/demo.zip) with the latest version of the demo notes
- Right click on any note in your tree under which you would like the demo notes to be imported
- Click "Import into note"
- Select the .zip archive to import it

## Manually Modifying the Database

Trilium provides a lot of flexibility, and with it, opportunities for advanced users to tweak it. If you need to explore or modify the database directly, you can use a tool such as [SQLite Browser](https://sqlitebrowser.org/) to work directly on the database file.

If you are doing any advanced development or troubleshooting where you manually modify the database, you might want to consider creating backups of your `document.db` file.

## How to Reset the Database

If you are experimenting with Trilium and want to return it to its original state, you can do that by deleting the current database. When you restart the application, it will generate a new database containing the original demo notes.

To delete the database, simply go to the [data directory](data-directory.md) and delete the `document.db` file (and any other files starting with `document.db`).

If you do not need to preserve any configurations that might be stored in the `config.ini` file, you can just delete all of the [data directory's](data-directory.md) contents to fully restore the application to its original state.