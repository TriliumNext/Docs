# Template

A template in Trilium serves as a predefined structure for other notes, referred to as instance notes. Assigning a template to a note brings three main effects:

1. **Attribute Inheritance**: All attributes from the template note are [inherited](attribute-inheritance.md) by the instance notes. Even attributes with `#isInheritable=false` are inherited by the instance notes, although only inheritable attributes are further inherited by the children of the instance notes.
2. **Content Duplication**: The content of the template note is copied to the instance note, provided the instance note is empty at the time of template assignment.
3. **Child Note Duplication**: All child notes of the template are deep-duplicated to the instance note.

## Example

A typical example would be a "Book" template note, which might include:

- **Promoted Attributes**: Such as publication year, author, etc. (see [promoted attributes](promoted-attributes.md)).
- **Outline**: An outline for a book review, including sections like themes, conclusion, etc.
- **Child Notes**: Additional notes for highlights, summary, etc.

![Template Example](images/template.png)

## Instance Note

An instance note is a note related to a template note.
This relationship means the instance note's content is initialized from the template, and all attributes from the template are inherited. 

To create an instance note through the UI:

%%{WARNING}%% Image not in Repo
![](api/images/qGovjbsV4FPX/template-create-instance-note.)

For the template to appear in the menu, the template note must have the `#template` label.
Do not confuse this with the `~template` relation, which links the instance note to the template note.
If you use [workspaces](workspace.md), you can also mark templates with `#workspaceTemplate` to display them only in the workspace.

Templates can also be added or changed after note creation by creating a `~template` relation pointing to the desired template note.

## Additional Notes

From a visual perspective, templates can define `#iconClass` and `#cssClass` attributes, allowing all instance notes (e.g., books) to display a specific icon and CSS style.

Explore the concept further in the [demo notes](database.md), including examples like the [Relation Map](relation-map.md), [Task Manager](task-manager.md), and [Day Notes](day-notes.md).

Additionally, see [default note title](default-note-title.md) for creating title templates. Note templates and title templates can be combined by creating a `#titleTemplate` for a template note.
