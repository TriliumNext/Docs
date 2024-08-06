# FAQ
Mac OS support
--------------

Originally, desktop builds of Trilium Notes has been available for Windows & Linux, but there has been a considerable demand for macOS build.

So I made one, but I underestimated the differences and specifics of Mac platform which seems to require special handling in several places. My lack of knowledge and frankly willingness to learn & code Mac specific functionality resulted in a current state where [Trilium does not integrate well into the OS](https://github.com/TriliumNext/Notes/issues/511) %%{WARNING}%%.

macOS build is from now on considered "unsupported". I will strive to keep it fundamentally functional, but I won't work on Mac specific features or integrations. Note that this is more of an acknowledgment of an existing state rather than sudden change of direction.

Of course, PRs are welcome.

Translation / localization support
----------------------------------

Trilium is currently available only in English. Translation to other languages is not planned in the near/medium term because it brings a significant maintenance overhead. This decision might be revisited once Trilium stabilizes into a more mature product.

For Chinese, there's an unofficial fork [here](https://github.com/Nriver/trilium-translation). Use at your own risk.

Multi user support
------------------

Common request is to allow multiple users collaborate, share notes etc. So far I'm resisting this because of these reasons:

*   it's a huge feature, or rather a Pandora's box of collaboration features like user management, permissions, conflict resolution, real-time editing of a note by multiple people etc. This would be a huge amount of work. Trilium Notes is project made mostly by one person in free time and that's unlikely to change in the future.
*   given its size it would probably pivot the attention away from my main focus which is a personal note-taking
*   the assumption that only single person has access to the app simplifies many things, or just outright makes them possible. In multi-user app, our [scripting](scripts.md) support would be a XSS security hole, while with the single user assumption it's an endless customizable tool.

How to open multiple documents in one Trilium instance
------------------------------------------------------

This is normally not supported - one Trilium process can open only a single instance of a [database](database.md). However, you can run two Trilium processes (from one installation), each connected to a separate document. To achieve this, you need to set a location for the [data directory](data-directory.md) in the `TRILIUM_DATA_DIR` environment variable and separate port on `TRILIUM_PORT` environment variable. How to do that depends on the platform, in Unix-based systems you can achieve that by running command such as this:

```text-plain
TRILIUM_DATA_DIR=/home/me/path/to/data/dir TRILIUM_PORT=12345 trilium 
```

You can save this command into a `.sh` script file or make an alias. Do this similarly for a second instance with different data directory and port.

Can I use Dropbox / Google Drive / OneDrive to sync data across multiple computers.
-----------------------------------------------------------------------------------

No.

These general purpose sync apps are not suitable to sync database files which are open and being worked on by another application. The result is that they will corrupt the database file, resulting in data loss and this message in the Trilium logs:

> SqliteError: database disk image is malformed

The only supported way to sync Trilium's data across the network is to use a [sync/web server](synchronization.md).

Why database instead of flat files?
-----------------------------------

Trilium stores notes in a [database](database.md) which is an SQLite database. People often ask why doesn't Trilium rather use flat files for note storage - it's fair question since flat files are easily interoperable, work with SCM/git etc.

Short answer is that file systems are simply not powerful enough for what we want to achieve with Trilium. Using filesystem would mean fewer features with probably more problems.

More detailed answer:

*   [clones](cloning-notes.md) are what you might call "hard directory link" in filesystem lingo, but this concept is not implemented in any filesystem
*   filesystems make a distinction between directory and file while there's intentionally no such difference in Trilium
*   files are stored in no particular order and user can't change this
*   Trilium allows storing note [attributes](attributes.md) which could be represented in extended user attributes but their support differs greatly among different filesystems / operating systems
*   Trilium makes links / relations between different notes which can be quickly retrieved / navigated (e.g. for [note map](note-map.md)). There's no such support in file systems which means these would have to be stored in some kind of side-car files (mini-databases).
*   Filesystems are generally not transactional. While this is not completely required for a note-taking application, having transactions make it way easier to keep notes and their metadata in predictable and consistent state.
