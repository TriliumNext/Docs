# Tree concepts
This page describes some basic concepts related to the tree structure of notes in Trilium.

Note
----

Note is a central entity in Trilium. See [Note](note.md) for details.

Branch
------

Branch describes note placement in the note tree - in essence it's a tuple of parentNoteId and noteId which says that given note is placed as a child into this parent note.

Each note can have more than one such branches, in other words any note can have multiple placements in the tree. For lack of better word we call this "[cloning](cloning-notes.md)".

Prefix
------

Prefix is branch (placement) specific title prefix for the note. Let's say you have your note placed into two different places in the tree, but you want to change the title a bit in one of the placements. For this you can use prefix.

To edit prefix, right-click on a note in the tree pane and choose "Edit branch prefix".

Prefix is not part of the note itself and thus is not encrypted when the note is protected. That can be useful when you want to keep part of the title in the tree visible even when protected for easier orientation.

Subtree
-------

Subtree is a set of notes consisting of a particular note (subtree root) and all its children, children of these children (= all its descendants). Some operations work on subtrees (e.g. export).
