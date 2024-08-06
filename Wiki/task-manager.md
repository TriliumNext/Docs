# Task-manager
Task Manager is a [promoted attributes](promoted-attributes.md) and [scripts](scripts.md) showcase present in the [demo notes](database.md).

Demo
----

![](images/task-manager.png)

Task Manager manages outstanding (TODO) tasks and finished tasks (non-empty doneDate attribute). Outstanding tasks are further categorized by location and arbitrary tags - whenever you change tag attribute in the task note, this task is then automatically moved to appropriate location.

Task Manager also integrates with [day notes](day-notes.md) - notes are [cloned](cloning-notes.md) into day note to both todoDate note and doneDate note (with [prefix](tree-concepts.md) of either "TODO" or "DONE").

Implementation
--------------

New tasks are created in the TODO note which has `~child:template` [relation](attributes.md) (see [attribute inheritance](attribute-inheritance.md)) pointing to the task template.

### Attributes

Task template defines several [promoted attributes](promoted-attributes.md) - todoDate, doneDate, tags, location. Importantly it also defines `~runOnAttributeChange` relation - [event](events.md) handler which is run on attribute change. This [script](scripts.md) handles when e.g. we fill out the doneDate attribute - meaning the task is done and should be moved to "Done" note and removed from TODO, locations and tags.

### New task button

There's also "button" note which contains simple script which adds a button to create new note (task) in the TODO note.

```text-plain
api.addButtonToToolbar({
    title: 'New task',
    icon: 'check',
    shortcut: 'alt+n',
    action: async () => {
        // creating notes is backend (server) responsibility so we need to pass
        // the control there
        const taskNoteId = await api.runOnBackend(async () => {
            const todoRootNote = await api.getNoteWithLabel('taskTodoRoot');
            const {note} = await api.createNote(todoRootNote.noteId, 'new task', '');

            return note.noteId;
        });

        // we got an ID of newly created note and we want to immediatelly display it
        await api.activateNewNote(taskNoteId);
    }
});
```

### CSS

In the demo screenshot above you may notice that TODO tasks are in red color and DONE tasks are green.

This is done by having this CSS [code note](code-notes.md) which defines extra CSS classes:

```text-plain
span.fancytree-node.todo .fancytree-title {
    color: red !important;
}

span.fancytree-node.done .fancytree-title {
    color: green !important;
}
```

This [code note](code-notes.md) has `#appCss` [label](attributes.md) which is recognized by Trilium on startup and loaded as CSS into the application.

Second part of this functionality is based in event handler described above which assigns `#cssClass` label to the task to either "done" or "todo" based on the task status.
