# Keyboard-shortcuts
This is supposed to be a complete list of keyboard shortcuts. Note that some of these may work only in certain contexts (e.g. in tree pane or note editor).

It is also possible to configure most keyboard shortcuts in Options -> Keyboard shortcuts. Using `global:` prefix, you can assign a shortcut which will work even without Trilium being in focus (requires app restart to take effect).

Note navigation
---------------

*   `UP`, `DOWN` - go up/down in the list of notes, `CTRL-SHIFT-UP` and `CTRL-SHIFT-DOWN` work also from editor
*   `LEFT`, `RIGHT` - collapse/expand node
*   `ALT+LEFT`, `ALT+RIGHT` - go back / forwards in the history
*   `CTRL+J` - show ["Jump to" dialog](note-navigation.md)
*   `CTRL+.` - scroll to current note (useful when you scroll away from your note or your focus is currently in the editor)
*   `BACKSPACE` - jumps to parent note
*   `ALT+C` - collapse whole note tree
*   `ALT+-` (alt with minus sign) - collapse subtree (if some subtree takes too much space on tree pane you can collapse it)
*   you can define a [label](attributes.md) `#keyboardShortcut` with e.g. value `Ctrl+I`. Pressing this keyboard combination will then bring you to the note on which it is defined. Note that Trilium must be reloaded/restarted (Ctrl+R) for changes to be in effect.

See demo of some of these features in [note navigation](note-navigation.md).

Tabs
----

*   `CTRL+click` - (or middle mouse click) on note link opens note in a new tab

Only in desktop (electron build):

*   `CTRL+T` - opens empty tab
*   `CTRL+W` - closes active tab
*   `CTRL+Tab` - activates next tab
*   `CTRL+Shift+Tab` - activates previous tab

Creating notes
--------------

*   `CTRL+O` - creates new note after the current note
*   `CTRL+P` - creates new sub-note into current note
*   `F2` - edit [prefix](note-navigation.md) of current note clone

Moving / cloning notes
----------------------

*   `CTRL+UP`, `CTRL+DOWN` - move note up/down in the note list
*   `CTRL+LEFT` - move note up in the note tree
*   `CTRL+RIGHT` - move note down in the note tree
*   `SHIFT+UP`, `SHIFT+DOWN` - multi-select note above/below
*   `CTRL+A` - select all notes in the current level
*   `SHIFT+click` - multi select note which you clicked on
*   `CTRL+C` - copies current note (or current selection) into clipboard (used for [cloning](cloning-notes.md)
*   `CTRL+X` - cuts current (or current selection) note into clipboard (used for moving notes)
*   `CTRL+V` - pastes note(s) as sub-note into current note (which is either move or clone depending on whether it was copied or cut into clipboard)
*   `DEL` - delete note / sub-tree

Editing notes
-------------

Trilium uses CKEditor 5 for the [text notes](text-notes.md) and CodeMirror 5 for [code notes](code-notes.md). Check the documentation of these projects to see all their built-in keyboard shortcuts.

*   `ALT-F10` - bring up inline formatting toolbar (arrow keys `<-`,`->` to navigate, `ENTER` to apply)
*   `ALT-F10` - again to bring up block formatting toolbar

*   `ENTER` in tree pane switches from tree pane into note title. Enter from note title switches focus to text editor. `CTRL+.` switches back from editor to tree pane.
*   `CTRL+K` - create / edit [external link](links.md)
*   `CTRL+L` - create [internal (note) link](links.md)
*   `ALT+T` - inserts current date and time at caret position
*   `CTRL+.` - jump away from the editor to tree pane and scroll to current note

Runtime shortcuts
-----------------

These are hooked in Electron to be similar to native browser keyboard shortcuts.

*   `F5`, `CTRL-R` - reloads trilium frontend
*   `CTRL+SHIFT+I` - show developer tools
*   `CTRL+F` - show search dialog
*   `CTRL+-` - zoom out
*   `CTRL+=` - zoom in

Other
-----

*   `ALT+O` - show SQL console (use only if you know what you're doing)
*   `ALT+M` - distraction-free mode - display only note editor, everything else is hidden
*   `F11` - toggle full screen
*   `CTRL+S` - toggle [search](search.md) form in tree pane
*   `ALT+A` - show note [attributes](attributes.md) dialog
