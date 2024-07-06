# Attributes
Note attributes are key-value records owned by (assigned to) given note.

There are 2 types of attributes:

*   Labels - simple key-value text record
*   Relation - specifies named relation (link) to another note

Sometimes we're talking about labels and relations - keep in mind that both of them are types of attributes.

![](images/attributes.png)

Labels
------

Labels can be used for several things:

*   as labels with optional value - e.g. when cataloguing books, you might add labels like #year=1999, #genre="sci-fi", #author="Neal Stephenson"
*   attributes can be used to configure some advanced features / settings - see below
*   plugins / scripts can use these to mark notes with some special values / metadata (e.g. [Weight Tracker](weight-tracker.md) will have "weight" attribute on [day notes](day-notes.md) based on whose it can create chart).

Labels can be used for [searching](search.md).

### Standard labels

The following labels are used for advanced configuration:

*   `disableVersioning` - disables auto-versioning. Useful for e.g. large, but unimportant notes - e.g. large JS libraries used for scripting
*   `calendarRoot` - marks note which should be used as root for [day notes](day-notes.md). Only one should be marked as such.
*   `archived` - notes with this label won't be visible by default in search results (also in Jump To, Add Link dialogs etc).
*   `excludeFromExport` - notes (with their sub-tree) won't be included in any note export.
*   `run` - defines on which events script should run. Possible values are:
    *   `frontendStartup` - when Trilium frontend starts up (or is refreshed).
    *   `backendStartup` - when Trilium backend starts up.
    *   `hourly` - run once an hour. You can use additional label `runAtHour` to specify at which hour.
    *   `daily` - run once a day.
*   `runAtHour` - On which hour should this run. Should be used together with `#run=hourly`. Can be defined multiple times for more runs during the day.
*   `runOnInstance` - define which trilium instance this should run on. Defaults to all instances.
*   `disableInclusion` - scripts with this label won't be included into parent script execution.
*   `sorted` - keeps child notes sorted (by title, alphabetically. See [Sorting](sorting.md)).
*   `top` - keeps this note at the top of the list within its parent (applies only on parents with `sorted` attribute).
*   `hidePromotedAttributes` - hide promoted attributes on this note.
*   `readOnly` - editor is in read only mode. Works only for text and code notes. See some use cases [here](https://github.com/TriliumNext/Notes/issues/371).
*   `autoReadOnlyDisabled` - text/code notes can be set automatically into read mode when they are too large. You can disable this behavior on per-note basis by adding this label to the note
*   `appCss` - marks CSS notes which are loaded into the Trilium application and can thus be used to modify Trilium's looks.
*   `appTheme` - marks CSS notes which are full Trilium themes and are thus available in Trilium options.
*   `cssClass` - the value of this label is then added as CSS class to the node representing the given note in the tree. This can be useful for advanced [themes](themes.md). Can be used in `template` notes.
*   `iconClass` - the value of this label is added as a CSS class to the icon on the tree, which can help visually distinguish the notes in the tree. An example might be `bx bx-home` - icons are taken from [boxicons](https://boxicons.com/). Can be used in [template](template.md) notes.
*   `pageSize`\- number of items per page in note listing.
*   `customRequestHandler` and `customResourceProvider` - see [Custom request handler](custom-request-handler.md)
*   `widget` - marks this note as a custom widget, which will be added to the Trilium component tree. See [Custom widget](custom-widget.md).
*   `workspace`, `workspaceIconClass`, `workspaceTabBackgroundColor`, `workspaceCalendarRoot` - see [Workspace](workspace.md)
*   `searchHome` - new search notes will be created as children of this note (otherwise they are created in [Day notes](day-notes.md))
*   `hoistedSearchHome` - new search notes will be created as children of this note when hoisted to some ancestor of this note
*   `inbox` - default inbox location for new notes - when you create a note using "new note" button in the sidebar, notes will be created as child notes in the note marked as with `#inbox` label.
*   `hoistedInbox` - default inbox location for new notes when hoisted to some ancestor of this note
*   `sqlConsoleHome` - default location of SQL console notes
*   `bookmarked` and `bookmarkFolder` - see [Bookmarks](bookmarks.md)
*   `shareXXX` labels - see [Sharing](sharing.md)
*   `keyboardShortcut` - can be defined as e.g. "Ctrl+I". Pressing this keyboard combination will then bring you to the note on which it is defined. Note that Trilium must be reloaded/restarted (Ctrl+R) for changes to be in effect.
*   `displayRelations` and `hideRelations` - comma delimited names of relations which should be displayed/hidden. All other relations will be hidden/visible.
*   `hideRelations` - comma delimited names of relations which should be hidden.
*   `titleTemplate` - see [Default note title](default-note-title.md).
*   `template` - this note will appear in the selection of available templates when creating new notes.
*   `toc` - `#toc` or `#toc=show` will force the table of contents to be shown, `#toc=hide` will force hiding it.
*   `color` - defines the color of the note in links, tree etc. Use any valid CSS value like `red` or `#f0a349`
*   `hideChildrenOverview` - Hides child notes from being displayed in the editor of the parent note
*   `viewType` - Allows setting the view of the child notes inside the editor to a grid or list. Possible values:
    *   `grid` - displays child notes in a grid
    *   `list` - displays child notes in a list

Relations
---------

Relation is a kind of link between two notes.

This could be used when you e.g. keep a book database, you can use relations to keep formal links between the book (note) and the book's author (note) by defining an "author" relation on the book note pointing to the author's note.

Relations are used also for some advanced scripting - like attaching scripts to events happening on certain note.

### Standard relations

[Events](events.md):

*   `runOnNoteCreation` - executes when note is created on backend. Use this relation if you want to run the script for all notes created under a specific subtree. In that case, create it on the subtree root note and make it inheritable. A new note created within the subtree (any depth) will trigger the script.
*   `runOnChildNoteCreation` - executes when new note is created under the note where this relation is defined
*   `runOnNoteTitleChange` - executes when note title is changed (includes note creation as well)
*   `runOnNoteChange` - executes when note is changed (includes note creation as well)
*   `runOnNoteDeletion` - executes when note is being deleted.
*   `runOnBranchCreation` and `runOnBranchDeletion` - executes when a branch is created/deleted. Branches are links between a parent and a child note, and are created when e.g. cloning or moving notes.
*   `runOnAttributeCreation` - executes when new attribute is created for the note which defines this relation
*   `runOnAttributeChange` - executes when the attribute is changed of a note which defines this relation. This is triggered also when the attribute is deleted

Other relations:

*   `template` - attached note's attributes will be inherited even without parent-child relationship. See [template](template.md) for details.
*   `renderNote` - notes of type "render HTML note" will be rendered using a code note (HTML or script) and it is necessary to point using this relation to which note should be rendered
*   `widget` - target of this relation will be executed and rendered as a widget in the sidebar
*   `shareXXX` relations described in [Sharing](sharing.md)

Multiplicity
------------

Attributes allow multiplicity - there can be multiple attributes with the same name. We're then calling such attributes "multivalued".

Attribute definitions / promoted attributes
-------------------------------------------

Special kind of labels are used to create "label/attribute" definitions. See [Promoted attributes](promoted-attributes.md) for details.

Attribute inheritance
---------------------

See [Attribute inheritance](attribute-inheritance.md).
