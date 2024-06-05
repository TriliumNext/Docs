## Standard inheritance

Every [[attribute|attributes]] has a flag called `isInheritable`. If this is true, then this attribute (key-value) is also applied to all its children notes, children's children notes etc. 

Example how this might be useful is `archived` label which hides its note from Jump to / Add link dialogs. Often times you want to archive some specific subtree, you can do this by making the `archived` label inheritable.

## Copying inheritance

A different kind of inheritance is achieved using `child:` attribute name prefix. We can define that when a note is created under a certain parent note then the new child note will automatically receive defined attributes. The difference from standard inheritance is that these are real new attributes which are completely independent of the parent and will be therefore kept even if the note is moved elsewhere in the note tree.

For defining the copy-attributes we use `child:` prefix in attribute name, the rest is defined normally. So as an example, when we create a child note in a note with `#child:exampleAttribute` label, then the child note will have `#exampleAttribute` label. This can be even chained, e.g. `#child:child:exampleAttribute`, in this case `#child:exampleAttribute` will be created in the child and `#exampleAttribute` will be created in the child of the child.

Which kind of attribute inheritance (or if any at all) should be used depends on the specific use case.

## Template inheritance

[[Attribute template|template]] could be also seen as a form of inheritance.
