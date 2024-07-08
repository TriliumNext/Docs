# Weight-tracker


The `Weight Tracker` is a [Script API](script-api.md) showcase present in the [demo document](document.md).

By adding `weight` as a [promoted attribute](promoted-attributes.md) to the [Day notes](day-notes.md) through its [template](template.md), you can aggregate the data and show a chart of weight change over time.

![](images/weight-tracker.png)

## Implementation

The `Weight Tracker` Note in the screenshot above is of type `Render Note`. That type of note doesn't have any useful content itself, the only purpose of it is to provide a place where a [script](scripts.md) can render its output.

Scripts for `Render Notes` are defined in a [relation](attributes.md) called `~renderNote`.  In this example, it's the `Weight Tracker`'s child `Implementation`. The Implementation consists of two [code notes](code-notes.md) that contain some HTML and JavaScript which loads all the notes with a `weight` attribute and displays their values in a chart.

To actually render the chart, we're using a third party library called [chart.js](https://www.chartjs.org/) which is imported as an attachment since it's not built into Trilium.

### Code

Here's the content of the script Note of type `JS Frontend`:

```js
async function getChartData() {
    const days = await api.runOnBackend(async () => {
        const notes = api.getNotesWithLabel('weight');
        const days = [];

        for (const note of notes) {
            const date = note.getLabelValue('dateNote');
            const weight = parseFloat(note.getLabelValue('weight'));

            if (date && weight) {
                days.push({ date, weight });
            }
        }

        days.sort((a, b) => a.date > b.date ? 1 : -1);

        return days;
    });

    const datasets = [
        {
            label: "Weight (kg)",
            backgroundColor: 'red',
            borderColor: 'red',
            data: days.map(day => day.weight),
            fill: false,
            spanGaps: true,
            datalabels: {
                display: false
            }
        }
    ];

    return {
        datasets: datasets,
        labels: days.map(day => day.date)
    };
}

const ctx = $("#canvas")[0].getContext("2d");

new chartjs.Chart(ctx, {
    type: 'line',
    data: await getChartData()
});
```

## How to remove Weight Tracker button from the top bar

In the link map of Weight Tracker, there is a note "Button". Open it and delete or comment out its contents. The Weight Tracker button will disappear after you restart Trilium.
