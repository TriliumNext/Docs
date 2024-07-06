# Code-notes
Trilium supports creating "code" notes, i.e. notes which contain some sort of formal code - be it programming language (C++, JavaScript), structured data (JSON, XML) or other types of codes (CSS etc.).

This can be useful for a few things:

*   computer programmers can store code snippets as notes with syntax highlighting
*   JavaScript code notes can be executed inside Trilium for some extra functionality
    *   we call such JavaScript code notes "scripts" - see [Scripts](scripts.md)
*   JSON, XML etc. can be used as storage for structured data (typically used in conjunction with scripting)

![](images/code-note.png)

Extra languages
---------------

Trilium supports syntax highlighting for many languages, but by default displays only some of them (to reduce the number of items). You can add extra languages in Options -> Code notes.

Code blocks
-----------

An alternative to the code note is a "code block" - feature of a text note which can add short snippets of code to the text editor. The disadvantage is that code blocks don't support syntax highlighting.

![](images/code-block.png)
