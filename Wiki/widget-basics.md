# Widget-Basics
### The Very Basics

Based on the information from [Frontend Basics](frontend-basics.md), the most basic widget we can make looks something like this.

```text-plain
class MyWidget extends api.BasicWidget {
    get position() {return 1;}
    get parentWidget() {return "left-pane"}

    doRender() {
        this.$widget = $("<div id='my-widget'>");
        return this.$widget;
    }
}

module.exports = new MyWidget();
```

If you put this in a `JS frontend` type code note, give it the `#widget` attribute and reload the page, you'll see that it runs fine with no errors. But how can we verify it worked? Open up devtools (`cmd`+`shift`+`i`) and check for the element using `document.querySelector("#my-widget")`. If you see an element, then you're all set. If you get `undefined`, something went wrong. Double check that you gave the note the `#widget` attribute.

Obviously, this is not the most helpful widget. It's not even a "Hello World" considering we can't actually see our element. Let's fix that.

### Rendering UI

Let's say that we just want to make a simple button that will show us a simple message when we click it. That should be easy enough.

First, we need to make our HTML a bit more complex to include the button. Thankfully this is easy with [jQuery](https://jquery.com/) because we can just pass an entire HTML string to it.

```text-plain
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

Make that change, and reload Trilium and you should see a really ugly looking button at the top-left of the left pane conflicting with the search bar. We can make that look a lot better very easily because Trilium includes [Box Icons](https://boxicons.com). Find and pick one from there, and copy the class name that it gives you. For this tutorial, I'll be using `bx bxs-magic-wand`. I'm also going to add the classes Trilium uses for the floating buttons in the tree list since that will make sure it matches any theme we use. I'd also recommend removing the text now that we have a fancy icon. Now my template looks like this:

```text-plain
const template = `<div id="my-widget"><button class="tree-floating-button bx bxs-magic-wand tree-settings-button"></button></div>`;
```

After reloading, that already looks a little bit better. But it's still in the wrong spot. We can fix that with a little bit of css. Thankfully [BasicWidget](https://triliumnext.github.io/Notes/frontend_api/BasicWidget.html) allows us to do this very easily with `this.cssBlock`.

```text-plain
const template = `<div id="my-widget"><button class="tree-floating-button bx bxs-magic-wand tree-settings-button"></button></div>`;

class MyWidget extends api.BasicWidget {
    get position() {return 1;}
    get parentWidget() {return "left-pane"}

    doRender() {
        this.$widget = $(template);
        this.cssBlock(`#my-widget {
            position: absolute;
            bottom: 40px;
            left: 60px;
            z-index: 1;
        }`)
        return this.$widget;
    }
}

module.exports = new MyWidget();
```

With that change, the button should now appear at the bottom left of the tree panel near the other action buttons.

### User Interaction

All that's left to do is add a click listener to show that message. Thankfully the [Script API](script-api.md) has a convenient method for showing messages shown below.

```text-plain
const template = `<div id="my-widget"><button class="tree-floating-button bx bxs-magic-wand tree-settings-button"></button></div>`;

class MyWidget extends api.BasicWidget {
    get position() {return 1;}
    get parentWidget() {return "left-pane"}

    doRender() {
        this.$widget = $(template);
        this.cssBlock(`#my-widget {
            position: absolute;
            bottom: 40px;
            left: 60px;
            z-index: 1;
        }`)
        this.$widget.find("button").on("click", () => api.showMessage("Hello World!"))
        return this.$widget;
    }
}

module.exports = new MyWidget();
```

Reload one last time, and go ahead and click your button. You'll get that classic Trilium toast with your `Hello World` message!
