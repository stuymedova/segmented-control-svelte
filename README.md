# Segmented Control

Segmented control is a set of two or more segments, each of which functions as a mutually exclusive button. It features a background, which can be animated with a sliding effect. Within the control, segments may have equal or variable width. The only direction supported currently is horizontal.

<img width="1153" alt="segmented-control-svelte" src="https://user-images.githubusercontent.com/53351370/150729107-af17b189-4b81-42ec-8fda-985699180c8e.png">

## Installation and Usage

**Installation**

To add a component to a SvelteKit project, run:
```shell
npm i segmented-control-svelte
```

**Usage**

Include component on a webpage by adding 
```js
import 'segmented-control-svelte/main.css' // Optionally, import a stylesheet
import { SegmentedControl, Segment } from 'segmented-control-svelte'
```
within the `script` tags of a Svelte file. You can further use the component as such:

```html
<SegmentedControl>
  <Segment id='first'>First</Segment>
  <Segment id='second'>Second</Segment>
</SegmentedControl>
```

The generated HTML will be as such:

```html
<div class="segmented-control" role="tablist" aria-orientation="horizontal">
  <button id="first" class="segmented-control-item selected" role="tab" aria-controls="" aria-disabled="false" aria-selected="true" tabindex="0">First</button>
  <button id="second" class="segmented-control-item" role="tab" aria-controls="" aria-disabled="false" aria-selected="false" tabindex="-1">Second</button>
  <div class="segmented-control-background" role="presentation" style="width: 75px; transform: translateX(2px);"></div>
</div>
```

## API

You can specify additional options for Segmented Control and each separate Segment.

**Segmented Control**

***selected***

Use this option to specify an index of an element to be selected by default, starting with 0.

```html
<SegmentedControl selected={1}>
  <Segment id='first'>First</Segment>
  <Segment id='second'>Second</Segment> <!-- This element will be selected initially -->
</SegmentedControl>
```

**Segment**

***id***

This option is *required*. For the component to work properly each segment must have a unique identifier.

```html
<SegmentedControl>
  <Segment id='first'>First</Segment>
  <Segment id='second'>Second</Segment>
</SegmentedControl>
```

***title***

Use this option to specify a title of a segment.

```html
<SegmentedControl>
  <Segment id='first' title='First' />
  <Segment id='second' title='Second' />
</SegmentedControl>
```

Alternatively, a title can be specified between component tags:

```html
<SegmentedControl>
  <Segment id='first'>First</Segment>
  <Segment id='second'>Second</Segment>
</SegmentedControl>
```

***disabled***

Use this option to disable a segment. In the example below, both segments will be disabled.

```html
<SegmentedControl>
  <Segment id='first' disabled>First</Segment>
  <Segment id='second' disabled={true}>Second</Segment>
</SegmentedControl>
```

***controls***

Use this option when using Segmented Control for toggling views (for accessibility purposes). Within the quotes specify the id of a controlled view.

<!-- TODO: provide a more complete example -->
```html
<SegmentedControl>
  <Segment id='first' controls='first-caption'>First</Segment>
  <Segment id='second' controls='second-caption'>Second</Segment>
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