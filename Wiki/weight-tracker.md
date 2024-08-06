# Weight-tracker

![screenshot of weight tracker](images/weight-tracker.png)

The `Weight Tracker` is a [Script API](script-api.md) showcase present in the [demo notes](database.md).

By adding `weight` as a [promoted attribute](promoted-attributes.md) in the [template](template.md) from which [day notes](day-notes.md) are created, you can aggregate the data and plot weight change over time.

## Implementation

The `Weight Tracker` note in the screenshot above is of the type `Render Note`. That type of note doesn't have any useful content itself. Instead it is a placeholder where a [script](scripts.md) can render its output.

Scripts for `Render Notes` are defined in a [relation](attributes.md) called `~renderNote`. In this example, it's the `Weight Tracker`'s child `Implementation`. The Implementation consists of two [code notes](code-notes.md) that contain some HTML and JavaScript respectively, which load all the notes with a `weight` attribute and display their values in a chart.

To actually render the chart, we're using a third party library called [chart.js](https://www.chartjs.org/) which is imported as an attachment, since it's not built into Trilium.

### Code

Here's the content of the script which is placed in a [code note](code-notes.md) of type `JS Frontend`:

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

## How to remove the Weight Tracker button from the top bar

In the link map of the `Weight Tracker`, there is a note called `Button`. Open it and delete or comment out its contents. The `Weight Tracker` button will disappear after you restart Trilium.
