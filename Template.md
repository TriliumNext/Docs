Template is a note which serves as a kind of "template" for other kind of notes (let's call them instance notes). 

Assignment of a template relation to a note brings these three effects:

* all attributes from the template note are [[inherited|attribute inheritance]] to the instance notes
  * note that even attributes with `#isInheritable=false` are inherited to the instance notes, but only inheritable attributes are then inherited to the children of instance notes
* note content is copied from the template note to the instance note (if the instance note content is empty at the time of template attribute assignment)
* all template's children notes are deep-duplicated to the instance note

## Example
A typical example would be a "Book" template note, which will:

* define some [[promoted attributes]] - e.g. publication year, author etc
* you can also create kind of outline of the book review in the note text - e.g. themes, conclusion etc. ..
* you can also create child notes for e.g. highlights, summary etc.

![](images/template.png)

## Instance note

And then we have instance note - this note has a [[relation|attributes]] to the "Book" template note which will cause that the template note text is used to initialize the instance note text and all attributes from the template note are inherited to the instance note.

You can create an instance note (i.e. note which uses a template) through the UI like this:

![](images/template-create-instance-note.png)

For the template to appear in the menu, the template note needs to have `#template` label (don't mistake it with `~template` relation which points from the instance note to the template note). If you use [[workspaces|workspace]], you can alternatively mark templates with `#workspaceTemplate` which will display them only in the workspace.

You can also add/change template notes after the note is created, simply create a relation `~template` pointing to the desired template note.

## Other remarks

From the visual perspective, template can define a `#iconClass` and `#cssClass` attributes so that all e.g. books are shown with a particular icon and CSS style.

You can check out the concept in the [[demo document|Document#demo-document]] in e.g. [[Relation map]], [[Task manager]] or [[Day notes]]. 

See also [[default note title]] which allows you to create templates for note titles. Note templates and title templates can be combined by creating a `#titleTemplate` for a template note.

