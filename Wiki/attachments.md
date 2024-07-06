# Attachments
A note can _own_ one or more attachments. The attachment is either an image or file which can be displayed/linked in the note which owns it.

The note is the exclusive owner of its attachments - they can't be linked from other notes. If a user copies the attachment link from one note to another, the attachment itself is copied and from then on lives an independent life.

Attachments is a feature available in Trilium since v0.61. Attachment is now a preferred way to include images into notes. Previously, an image had to be an independent note which could be then displayed in multiple notes, but this approach proved to be complicated. Image as notes still remains as an option, and is a more suitable choice in some cases (e.g. when the particular image is sort of standalone). It is possible to convert an image to an attachment and vice versa.

Image attachments are expected to be linked in the owning text note. If it's not linked, it will get deleted in a configurable timeout.
