### Description 

This repository is just a workaround to support filling/shadowing of line charts.

Usage example:

```JSX
import React from "react";
import { Chart } from 'marme1ad/react-charts-fill'

const defs = (
    <defs>
        <linearGradient id="line-gradient" x1="0" x2="0" y1="1" y2="0">
            <stop offset="0%" stopColor="#FFAEBF" />
            <stop offset="100%" stopColor="#B783FF" />
        </linearGradient>
        <linearGradient id="shadow-gradient" x1="0" x2="0" y1="0" y2="1">
            <stop offset="0%" stopColor="#FFAEBF" />
            <stop offset="90%" stopColor="#FFFFFF" />
        </linearGradient>
    </defs>
)

const TheChart = () => {
    let data = [
        {
            label: "Total",
            data: [
                ["04-01", 10], ["04-02", 20], ["04-03", 15], ["04-04", 40], ["04-05", 0], ["04-06", 20], ["04-05", 65]
            ]
        }
    ];

    const axes = React.useMemo(
        () => [
            { primary: true, type: 'ordinal', position: 'bottom', show: true },
            { type: 'linear', position: 'left', hardMin: 0, show: true }
        ],
        []
    )

    const getSeriesStyle = React.useCallback(
        series => ({
            showShadow: true,
            color: `url(#line-gradient)`,
            fill: `url(#shadow-gradient)`,
            opacity: 1,
            fillOpacity: 0.7,
        }),
        []
    )

    return (
        <Chart className="app-custom-chart" data={data} axes={axes}
            tooltip={tooltip}
            getSeriesStyle={getSeriesStyle}
            primaryCursor={{
                showLine: false
            }}
            renderSVG={() => defs} />
    )
}

export default TheChart;
```

### react-charts

[react-charts](https://github.com/tannerlinsley/react-charts) is licensed under the [MIT License](https://github.com/tannerlinsley/react-charts/blob/master/LICENSE).

Changes/adjustments done:

- `Line$1` defintion is changed to have possibility to set up `fill` for the area under the line charts (everything related to `showShadow`, `shadowPath`, `shadowPathProps`, `renderedShadowPathProps`).
