# Text Notes

Trilium utilizes the powerful [CKEditor 5](https://ckeditor.com/ckeditor-5/) as its text editing component.

## Formatting Options

The Trilium text note interface does not display toolbars or formatting options by default. These can be accessed by:

%%{WARNING}%% Image does not exist in repo
![](api/images/aQT4C1G1rjUk/text-notes-formatting-inline.p)

1. Selecting text to bring up an inline toolbar.

%%{WARNING}%% Image does not exist in repo
![](api/images/aQT4C1G1rjUk/text-notes-formatting-block.pn)

2. Clicking on the block toolbar.

## Read-Only vs. Editing Mode

Text notes are usually opened in edit mode. However, they may open in read-only mode under the following circumstances:

- The note is long and would take time to load, so it is opened in read-only mode by default for quicker access.
- The note has a `readOnly` [label](attributes.md).

In both cases, it is possible to switch back to editable mode.

## General Formatting

Since Trilium uses CKEditor, all of its formatting options are available here. You may use the graphical toolbar shown above, or enter formatting such as markdown markdown directly in the text. Examples include:

- **Bold**: Type `**text**` or `__text__`
- _Italic_: Type `*text*` or `_text_`
- `Code`: Type \`text\`
- ~Strikethrough~: Type `~~text~~`

### Lists

- Bulleted list: Start a line with `*` or `-` followed by a space
- Numbered list: Start a line with `1.` or `1)` followed by a space
- To-do list: Start a line with `[ ]` for an unchecked item or `[x]` for a checked item

### Blocks

- Block quote: Start a line with `>` followed by a space

### Multi-Line Code Blocks

To create a multi-line code block, start a line with "\`\`\`[lang]", for example:

```js
if (1 > 2) {
    console.log("Error in the matrix");
}
```

### Headings

Create headings by starting a line with `##` for heading 2, `###` for heading 3, and so on up to heading 6. Note that `#` is reserved for the title.

### Horizontal Line

Insert a horizontal line by starting a line with `---`.

## Markdown & Autoformat

CKEditor supports a markdown-like editing experience, recognizing syntax and automatically converting it to rich text.

Complete documentation for this feature is available in the [CKEditor documentation](https://ckeditor.com/docs/ckeditor5/latest/features/autoformat.html).

If autoformatting is not desirable, press `CTRL-Z` to revert the text to its original form.

Note: The use of `#` for Heading 1 is not supported because it is reserved for the title. Start with `##` for Heading 2. More information is available [here](https://ckeditor.com/docs/ckeditor5/latest/features/headings.html#heading-levels).

## Math Support

Trilium provides math support through [KaTeX](https://katex.org/).

## Cutting Selection to Sub-Note

When editing a document that becomes too large, you can split it into sub-notes:

1. Select the desired text and cut it to the clipboard.
2. Create a new sub-note and name it.
3. Paste the content from the clipboard into the sub-note.

Trilium can automate this process. The heading is automatically detected and the new sub-note is named accordingly. You can also assign a keyboard shortcut for this action.

## Including a Note

Trilium can automate this process. Select some text within the note, and in the selection toolbar, click the scissors icon for the "cut & pasted selection to sub-note" action. The heading is automatically detected and the new sub-note is named accordingly. You can also assign a keyboard shortcut for this action.

This functionality is available through the block toolbar icon.
