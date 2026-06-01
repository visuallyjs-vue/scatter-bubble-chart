### About this Demo

This Vue application demonstrates **Scatter and Bubble Charts** built with **VisuallyJS**.

### VisuallyJS Components Used

The demo utilizes several components from the `@visuallyjs/browser-ui-vue` package:

- **ScatterChartComponent**: Used for rendering scatter plots.
- **BubbleChartComponent**: Used for rendering bubble charts.

### Component Options

Each chart component receives an `options` object that configures its behavior and appearance. Common options include:

- **axes**: Configuration for the X and Y axes.
- **series**: Data series configuration (colors, labels, marker styles).
- **inverted**: Set to `true` to swap the X and Y axes.

### CSS Requirement

For the VisuallyJS components to render correctly, the standard VisuallyJS stylesheet must be included in the project. In this demo, it is imported in `src/main.js`:

```javascript
import "@visuallyjs/browser-ui/css/visuallyjs.css"
```
