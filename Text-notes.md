Trilium uses awesome [CKEditor 5](https://ckeditor.com/ckeditor-5/) as its editing component. 

## Formatting

Trilium text note interface doesn't show any toolbars or formatting options by default, these needs to be brought up by:

1) selecting text will bring up an inline toolbar:

![](images/text-notes-formatting-inline.png)

2) clicking on the block toolbar:

![](images/text-notes-formatting-block.png)

## Read only vs. editing mode

Text notes are normally opened in edit mode, however there are two cases when they are open in read-only mode:

* they are long and thus would take time to load so by default we open them as read only which is much quicker
* or the note has `readOnly` [[label|attributes]]

In both cases, it is possible to switch to editable mode again.

## General Formatting

Trilium uses the CKEditor, so any formatting that the CKEditor supports should be available in Trilium. For example:

**Bold** – Type `**text**` or `__text__`

*Italic* – Type `*text*` or `_text_`

`Code` – Type \`text`

~~Strikethrough~~ – Type `~~text~~`

### Lists

* Bulleted list – Start a line with `*` or `-` followed by a space

1. Numbered list – Start a line with `1.` or `1)` followed by a space

[ ] To-do list – Start a line with `[ ]` or `[x]` followed by a space to insert an unchecked or checked list item, respectively


###  Blocks

> Block quote – Start a line with `>` followed by a space

```Multi-line Code block``` – Start a line with ```


###  Other

Headings – Start a line with `##` or `###` followed by a space to create a heading 1, heading 2, or heading 3 (up to heading 6 if options defines more headings)

Note: Trilium only accepts headings with `##` and more because `#` is reserved for the title

Horizontal line – Start a line with `---`
--- 

## Markdown & Autoformat

CKEditor supports markdown-like editing experience. It recognizes syntax and automatically converts it to rich text. See it in action:

[[gifs/autoformat.gif]]
Complete documentation for this feature is available in [CKEditor documentation](https://ckeditor.com/docs/ckeditor5/latest/features/autoformat.html).

If the autoformat is not desirable for what you just wrote, you can press `CTRL-Z` which will un-autoformat the text to its original form.

Note that the use of `#` for Heading1 style is not supported because the editor assumes that is used for the title, start with `##` for Heading2. Explanation [here](https://ckeditor.com/docs/ckeditor5/latest/features/headings.html#heading-levels).

## Math support

Trilium provides Math support with the help of KaTex:

[[gifs/math.gif]]

## Cut selection to sub-note
One of the common situations in Trilium is when you're editing a document, and it gets somewhat large, so you start splitting it up into sub-notes - the process is essentially like this:

* select the desired piece of text and cut it into clipboard
* create new sub-note & give it name
* paste the content from clipboard into sub-note

Trilium provides a way to automate this:

[[gifs/cut-to-subnote.gif]]

You can notice how heading "Formatting" is automatically detected and new sub-note is named "Formatting".

It is also possible to assign a keyboard shortcut for this action.

## Include note

Text notes can "include" another note as a read only widget. This can be useful for e.g. including a dynamically generated chart (from scripts & "render HTML" note) or other more advanced use cases.

This functionality is available in the block toolbar icon.

![image](https://user-images.githubusercontent.com/617641/161419847-7709db0e-04cf-4157-b6ec-0ef6cdaa3f74.png)
