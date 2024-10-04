# Introduction to Widget Development

This guide will walk you through creating a basic widget inside Trilium. By following these steps, you'll learn how to build a simple UI element that interacts with the user.

### Step 1: The Basic Widget Structure

To start, we'll create the most basic widget possible. 
Here's a simple example:

```js
class MyWidget extends api.BasicWidget {
    get position() { return 1; }
    get parentWidget() { return "left-pane"; }
    
    doRender() {
        this.$widget = $("<div id='my-widget'>");
        return this.$widget;
    }
}

module.exports = new MyWidget();
```

To implement this widget:

1. Create a new `JS Frontend` note in Trilium and paste in the code above.
2. Assign the `#widget` [attribute](attributes.md) to the [note](note.md).
3. Restart Trilium or reload the window.

To verify that the widget is working, open the developer tools (`Cmd` + `Shift` + `I`) and run `document.querySelector("#my-widget")`. If the element is found, the widget is functioning correctly. If `undefined` is returned, double-check that the [note](note.md) has the `#widget` [attribute](attributes.md).

### Step 2: Adding an UI Element

Next, let's improve the widget by adding a button to it.

```js
const template = `<div id="my-widget"><button>Click Me!</button></div>`;

class MyWidget extends api.BasicWidget {
    get position() {return 1;}
    get parentWidget() {return "left-pane"}

    doRender() {
        this.$widget = $(template);
        return this.$widget;
    }
}

module.exports = new MyWidget();
```

After making this change, reload Trilium. You should now see a button in the top-left corner of the left pane.

### Step 3: Styling the Widget

To make the button more visually appealing and position it correctly, we'll apply some custom styling. Trilium includes [Box Icons](https://boxicons.com), which we'll use to replace the button text with an icon.
For example the `bx bxs-magic-wand` icon.

Here's the updated template:

```js
const template = `<div id="my-widget"><button class="tree-floating-button bx bxs-magic-wand tree-settings-button"></button></div>`;
```

Next, we'll adjust the button's position using CSS:

```js
class MyWidget extends api.BasicWidget {
    get position() { return 1; }
    get parentWidget() { return "left-pane"; }
    
    doRender() {
        this.$widget = $(template);
        this.cssBlock(`#my-widget {
            position: absolute;
            bottom: 40px;
            left: 60px;
            z-index: 1;
        }`);
        return this.$widget;
    }
}

module.exports = new MyWidget();
```

After reloading Trilium, the button should now appear at the bottom left of the left pane, alongside other action buttons.

### Step 4: Adding User Interaction

Let’s make the button interactive by showing a message when it’s clicked. We'll use the `api.showMessage` method from the [Script API](script-api.md).

```js
class MyWidget extends api.BasicWidget {
    get position() { return 1; }
    get parentWidget() { return "left-pane"; }
    
    doRender() {
        this.$widget = $(template);
        this.cssBlock(`#my-widget {
            position: absolute;
            bottom: 40px;
            left: 60px;
            z-index: 1;
        }`);
        this.$widget.find("button").on("click", () => api.showMessage("Hello World!"));
        return this.$widget;
    }
}

module.exports = new MyWidget();
```

Reload the application one last time. When you click the button, a "Hello World!" message should appear, confirming that your widget is fully functional.
