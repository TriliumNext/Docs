# Sharing
Trilium provides a feature to share selected notes as **publicly accessible** read only documents.

The basic prerequisite for this feature is to have a [server installation](server-installation.md) - this is where the notes will be hosted from.

Share note
----------

Click on the "shared" switch, URL appears on which you can click.![](images/share-single-note.png)

And this is the opened link:

![](images/share-single-note-web.png)

The URL refers to the localhost (127.0.0.1) because there's no configured sync server.

Share a note subtree
--------------------

Sharing a note actually shares a whole subtree of notes, the note shown above just didn't have any children.

If I share the whole "Formatting" subtree then the page looks like this:

![](images/share-multiple-notes-web.png)

You can see a basic navigation on the right. With this you can create small websites.

Showing list of all shared notes
--------------------------------

You can click on the "Show Shared Notes Subtree" to see the list of all shared notes

Security
--------

The notes you share are published on the open internet and can be accessed by anybody. The fact that the URLs look randomly does not provide real security guarantees. Please don't put sensitive information into shared notes.

There is an opt-in feature to require a username/password, see `#shareCredentials` below.

Advanced options
----------------

### Styling the shared notes

The default shared page is pretty rudimentary. In case you want to style it more nicely, you can:

*   add a `~shareCss` relation to a CSS code note which will be linked in the shared page
    *   in case you want this to apply to the whole subtree, don't forget to make the label inheritable
    *   the linked CSS code note needs to be also in the shared subtree. If you want to hide it from left tree navigation, add `#shareHiddenFromTree` label to the CSS code note.
*   if you make extensive styling changes, then it's recommended to use `#shareOmitDefaultCss` on the shared subtree so that you don't need to override the default stylesheet (this will also avoid problems in the future when the default CSS changes).

### Scripting

It's possible to inject a JavaScript note to the shared note using `~shareJs` relation.

In case you want to access e.g. attributes or traverse the tree in the linked JavaScript note, you can use the API available through global [`fetchNote(noteId = current)` function](https://github.com/TriliumNext/Notes/blob/master/src/public/app/share.js), e.g.:

```text-plain
const currentNote = await fetchNote();
const parentNote = await fetchNote(currentNote.parentNoteIds[0]);

for (const attr of parentNote.attributes) {
    console.log(attr.type, attr.name, attr.value);
}
```

### Creating human-readable URL aliases

Shared notes are accessible using URLs like `http://domain/share/knvU8aJy4dJ7`, where the last part is the note's ID.

You can add `#shareAlias` to individual notes to make the URLs nicer, e.g. `#shareAlias=highlighting` will make the URL look like `http://domain/share/highlighting`.

Note that you are responsible for keeping the aliases unique.

Using "subpaths", i. e. to declare an alias with `/` within, is not supported.

### Seeing all shared notes

All shared notes are grouped under automatically managed "Shared Notes" note. Besides seeing what's shared, you can also effectively share/unshare notes by cloning/moving them from/to this note.

![](images/shared-list.png)

### Favicon

You can define a custom favicon used for shared pages by create a relation `~shareFavicon` pointing to the file note containing the favicon (in e.g. the `ico` format).

### Sharing a note as the root

You can add the `#shareRoot` attribute to a folder or note, and it will be linked when you visit [http://domain/share](http://domain/share). This can make it easier to use Trilium as a fully-fledged website because you can create a note to act as a "home-page".

Consider also combining this with `#shareIndex` which will display the list of all shared notes.

### Protecting shared notes with a password

It is possible to optionally protect shared notes with credentials.

To do that, create a label in the format `#shareCredentials="username:password"` to a note which you want to protect. Typically, you want to make the whole sub-tree protected like that, so don't forget to make this label inheritable.

Keep in mind that the default state is public, so make sure everything you need to protect has this label (either owned or inherited).

Note titles of password protected notes may appear in the links and navigation from unprotected notes.

Password-protecting shared notes is available since 0.54.

### Other options

*   if a note has `#shareRaw` label, the note will be shared raw, without HTML wrapper
*   if a note has `#shareDisallowRobotIndexing` label, it will carry `<meta name="robots" content="noindex,follow" />` meta tag and `X-Robots-Tag: noindex` header, which will advise crawlers to skip this page
*   if a text note has `#shareIndex` label, its content will display a list of all shared note roots (since v0.57)

Limitations
-----------

Shared notes functionality is compared to standard functionality very limited.

The not exhaustive list of **what is missing** is:

*   relation map support
*   book notes show only children note list
*   code notes have no highlighting
*   note tree is static
*   Protected notes cannot be shared
*   include notes

Some of these limitations might be removed/mitigated in the future.
