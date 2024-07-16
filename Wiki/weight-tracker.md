# Weight-tracker
Weight Tracker is a [Script API](script-api.md) showcase present in the [demo notes](database.md).

[Day notes](day-notes.md) shows (among others) how we have "weight" [promoted attribute](promoted-attributes.md) in the day note [template](template.md). This then aggregates the data and shows a nice chart of weight change in time.

Demo
----

![](images/weight-tracker.png)

How to remove Weight Tracker button from the top bar
----------------------------------------------------

In the link map of Weight Tracker, there is a note "Button". Open it and delete or comment out its contents. Weight Tracker button will disappear after you close and open the app.

Implementation
--------------

Note "Weight Tracker" in the screenshot above is of type "Render HTML note". Such note doesn't have any useful content itself, the only purpose of it is to provide a place where some [script](scripts.md) can render some output. This script is defined in [relation](attributes.md) `renderNote` - coincidentally it's the Weight Tracker's child `Implementation`.

This Implementation [code note](code-notes.md) then contains some HTML and JavaScript which loads all the notes with "weight" attribute and displays them in a chart. To actually render chart we're using third party library [chart.js](https://www.chartjs.org/) which is imported as an attachment (it's not built-in into Trilium).

### JS code

To get an idea of the script, here's the "JS code" note content:

```text-plain
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
