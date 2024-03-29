# Segmented Control

Segmented Control is a set of two or more Segments, each of which functions as a mutually exclusive button. It features a background, which can be animated with a sliding effect.

<img width="1153" alt="segmented-control-svelte" src="https://user-images.githubusercontent.com/53351370/150729107-af17b189-4b81-42ec-8fda-985699180c8e.png">

## Installation and Usage

**Installation**

To add a component to a Svelte/SvelteKit project, run:
```shell
npm i segmented-control-svelte
```

**Usage**

Include component on a webpage by adding
```js
import 'segmented-control-svelte/main.css' // Optional, alternatively use darkMode.css or a custom stylesheet
import { SegmentedControl, Segment } from 'segmented-control-svelte'
```
within the `script` tag of a Svelte file. You can further use the component as such:

```html
<SegmentedControl>
  <Segment>First</Segment>
  <Segment>Second</Segment>
</SegmentedControl>
```

The generated HTML will be as such:

```html
<div class="segmented-control" role="tablist" aria-orientation="horizontal">
  <button class="segment selected" role="tab" aria-selected="true" aria-disabled="false" tabindex="0">First</button>
  <button class="segment" role="tab" aria-disabled="false" aria-selected="false" aria-disabled="false" tabindex="-1">Second</button>
  <div class="segmented-control-background" role="presentation" style="width: 75px; transform: translateX(2px);"></div>
</div>
```

## API

You can specify additional options for Segmented Control and each separate Segment.

**Segmented Control**

***selectedIndex***

Use this option to specify an index of an element to be selected by default, starting with 0.

```html
<SegmentedControl selectedIndex={1}>
  <Segment>First</Segment>
  <Segment>Second</Segment> <!-- This element will be selected initially -->
</SegmentedControl>
```

You can bind to this value to have changes to the selected index be reflected both in the Segmented Control component and any other part of the interface that uses it.

```html
<script>
  import 'segmented-control-svelte/main.css'
  import { SegmentedControl, Segment } from 'segmented-control-svelte'

  let segmentedControlSelectedIndex = 1
</script>

<SegmentedControl bind:selectedIndex={segmentedControlSelectedIndex}>
  <Segment>First</Segment>
  <Segment>Second</Segment>
</SegmentedControl>

<p>Index of a selected element: {segmentedControlSelectedIndex}</p>
```

***orientation***

Use this option to specify orientation of the Segmented Control. Accepted options are "horizontal" and "vertical". Default orientation is "horizontal".

```html
<SegmentedControl orientation='vertical'>
  <Segment>First</Segment>
  <Segment>Second</Segment>
</SegmentedControl>
```

**Segment**

***label***

Use this option to specify a Segment's label.

```html
<SegmentedControl>
  <Segment label='First' />
  <Segment label='Second' />
</SegmentedControl>
```

Alternatively, a label can be specified between component tags:

```html
<SegmentedControl>
  <Segment>First</Segment>
  <Segment>Second</Segment>
</SegmentedControl>
```

***isDisabled***

Use this option to disable selection of a Segment.

```html
<SegmentedControl>
  <Segment>First</Segment>
  <Segment isDisabled={true}>Second</Segment>
</SegmentedControl>
```

## Demo

Launch a demo by running in the terminal:

```shell
git clone --depth=1 https://github.com/stuymedova/segmented-control-svelte . # Clone the latest commit from this repository to your current directory
npm install
npm run dev
```

The demo will be available at http://localhost:3000. Navigate to `src/routes/index.svelte` to make any changes.
