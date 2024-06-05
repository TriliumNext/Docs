Trilium by default comes with few color themes, with white being the default. To switch to dark theme, you just need to go to Options (top-left - it's the app icon) -> Appearance tab and change the theme.

This is what it looks like:

[[images/dark-theme.png]]

## Custom CSS themes

Trilium provides a concept of custom user theme. You can make yourself one by creating a CSS [[code note|code notes]] and annotating it with `#appTheme=my-theme-name` [[label|attributes]].

You can see an example of what you can put there below:

```css
@font-face {
  font-family: 'Raleway';
  font-style: normal;
  font-weight: 400;
  src: url('/custom/fonts/raleway.woff2') format('woff2');
}

:root {
    --main-font-family: 'Raleway' !important;
    --main-font-size: normal;
    --tree-font-family: inherit;
    --tree-font-size: normal;
    --detail-font-family: inherit;
    --detail-font-size: normal;
    --detail-text-font-family: 'Garamond' !important;

    --main-background-color: #404552;
    --main-text-color: #AFB8C6;
    --main-border-color: #AFB8C6;
    --accented-background-color: #383C4A;
    --more-accented-background-color: #2F343F;
    --header-background-color: #383C4A;
    --button-background-color: #2F343F;
    --button-disabled-background-color: #404552;
    --button-border-color: #333;
    --button-text-color: #AFB8C6;
    --button-border-radius: 2px;
    --primary-button-background-color: #6c757d;
    --primary-button-text-color: white;
    --primary-button-border-color: #6c757d;
    --muted-text-color: #86919F;
    --input-text-color: #AFB8C6;
    --input-background-color: #404552;
    --hover-item-text-color: white;
    --hover-item-background-color: #4877B1;
    --active-item-text-color: white;
    --active-item-background-color: #4877B1;
    --menu-text-color: #AFB8C6;
    --menu-background-color: #383C4A;
    --tooltip-background-color: #383C4A;
    --link-color: lightskyblue;
    --modal-background-color: #404552;
    --modal-backdrop-color: black;
    --scrollbar-border-color: rgba(175, 184, 198, 0.5);
}

body .note-detail-text {
    font-size: 120%;
}

body .CodeMirror {
    filter: invert(100%) hue-rotate(180deg);
}
```

We define a custom font (provided by [[custom request handler]]) and then just define a bunch of CSS variables. These variables are then used in Trilium's CSS stylesheets. You can also use standard CSS selectors for further customization (open dev tools using `CTRL-SHIFT-I` to help with that), but keep in mind that HTML structure can change in future releases which might break your selectors. For that reason it is better to restrict yourself to use CSS variables as much as possible.

To activate your custom theme, go to Options -> Appearance. In the select box you should see all notes (themes) labeled with `appTheme`.

If you make a change to your theme, you should reload the frontend by pressing `CTRL-R` so the changes will take effect.

CSS themes can be exported in .tar archive and shared to other users. Importing CSS themes from untrusted sources is not advised since the archive can also contain executable [[scripts]] which could be potentially harmful.

You can find an example user theme *Steel Blue* in the [[demo document|Document#demo-document]]:

[[images/steel-blue.png]]

## Custom CSS

Trilium also allows you to create custom CSS not associated with a theme. This can be useful in the context of [[scripting|scripts]] where you may want to e.g. change colors of notes in the tree (as used in [[Task manager]]).

To do this, just create a [[code note|code notes]] with CSS type, put your custom CSS code into the note's content and create "appCss" [[label|Attributes]]. When Trilium frontend starts, all notes with "appCss" label are appended in the style element of the Trilium HTML page.

Once you made your changes, you can reload the Trilium frontend by pressing CTRL-R after which the changes will take effect.

[[images/app-css.png]]

## Styling the tree

If you want to give some specific notes special styling in the tree, you can give them `cssClass` [[label|attributes]] which is then put into the node representing given note in the tree.

There's also an `iconClass` using which you can define custom icons for notes in the tree - you can either use supplied ones from [boxicons](https://boxicons.com/) (e.g. `bx bx-home`) or you can define your own CSS classes.
Some of those are actually different. So you have `bx bxs-piano`for instance instead of `bx bx-piano`.
On the boxicons site, you can find out, looking at the font tab, after u opened a file, how its called.


`iconClass` and `cssClass` are especially powerful when used with [[template]].

You can also create specific styling for given note types (and mime types). For example, file note containing PNG image will have these classes in the tree: `type-image mime-image-png`.

## User-provided themes

Some users made their custom themes publicly available. For a gallery of user themes, see [[Theme gallery]].

## Asset path

In case you want to use some built-in assets like `/assets/v0.57.0-beta/images/icon-grey.png` but want to avoid specifying the version, you can use a `vX` alias - in this case `/assets/vX/images/icon-grey.png`.