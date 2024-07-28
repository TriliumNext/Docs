# Anonymized Database

![screenshot of advanced settings](images/anonymization.png)

In certain scenarios, understanding the structure of a database is crucial for troubleshooting issues. However, sharing your actual [database](database.md) file with personal notes is not advisable. To address this, Trilium offers a feature to anonymize the database. This feature can be accessed via Menu -> Options -> Advanced tab.

This feature creates a copy of your database with all sensitive data removed. Specifically, it strips out note titles, contents, revisions, history, and some non-system attributes while retaining the overall structure and metadata, such as modification dates. After anonymization, the database undergoes a [vacuuming process](https://sqlite.org/lang_vacuum.html) to ensure no sensitive data remnants remain in the file. The anonymized database is saved in the `anonymized` directory within the [data directory](data-directory.md), making it safe to share with bug reports.

## Command Line Anonymization

If your [database](database.md) is corrupted to the point where Trilium cannot start, the anonymization process can still be executed via the command line:

```sh
node src/anonymize.js
```

Run this command from the directory containing Trilium's source files, typically found in the `resources/app` directory for desktop builds.
