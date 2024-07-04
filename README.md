# Trilium Next documentation

This is an export of the upsteam [Zadam Wiki][0] for Trilium Notes. It's been converted from Github wiki format to markdown with some light rearranging to make for better presentation when imported into Trilium. It's anticipdated that in time this will supercede Zadam Wiki.

## Importing

To import these docs into your own Trilium instance:

1. Download archive from main branch of this repo:
https://github.com/TriliumNext/Docs/archive/refs/heads/main.zip
2. In Trilim create a new note to act as branch for the docs
3. Right-click >> Import into note >> select downloaded `Docs-main.zip`
  a. optionally uncheck "Shrink images"

### Optional cleanup
- delete `!!!meta.json`
- Move `images` node down to the bottom (instead of dragging, it's easier to move out to parent node than back into Wiki. It will go to end of list automatically).

For new releases delete the old docs note tree and start fresh, or you'll get duplicates.

[0]: https://github.com/zadam/trilium/wiki
