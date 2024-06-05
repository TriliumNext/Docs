[[Text|Text notes]] or [[code|Code notes]] can be set to be read-only. In such case only read view is presented to the user with the option of editing the note if needed.

## Setting read only view with label

You can set the note as read only by adding [[label|attributes]] `readOnly`.

## Auto read only

If the note is too large then Trilium will automatically set the note as readOnly as an optimization - displaying such long notes can take a long time in editing mode and this might unnecessarily slow down operation even if editing is not necessary.

If you want to keep specific note automatically editable, you can add [[label|attributes]] `autoReadOnlyDisabled`.