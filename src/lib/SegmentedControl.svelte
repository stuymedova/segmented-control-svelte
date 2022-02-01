<script>
  import { setContext, onMount } from 'svelte'
  import { writable } from 'svelte/store'

  export let selected = 0

  let selectedIndex = writable(selected)
  let segments = []
  let indexIterator = -1
  let backgroundLength = 0
  let backgroundOffset = 0

  setContext('SegmentedControl', {
    selectedIndex,
    setIndex: () => {
      indexIterator += 1
      return indexIterator
    },
    addSegment: ({ index, disabled, length, offset }) => {
      if (index === $selectedIndex) {
        backgroundLength = length
        backgroundOffset = offset
      }
      segments = [...segments, { index, disabled, length, offset }]
    },
    setAsSelected: (nextIndex) => {
      $selectedIndex = nextIndex

      if ($selectedIndex < 0) {
        $selectedIndex = 0
      } else if ($selectedIndex >= segments.length) {
        $selectedIndex = segments.length - 1
      }

      if (segments[$selectedIndex].disabled !== true) {
        backgroundLength = segments[$selectedIndex].length
        backgroundOffset = segments[$selectedIndex].offset
      }
    }
  })

  onMount(() => {
    if (segments.length < 2) {
      console.error('Segmented Control: For the component to function properly, provide two or more Segments.')
    }
  })
</script>


<div 
  class='segmented-control' 
  role='tablist'
  aria-orientation='horizontal'
  {...$$restProps}
  on:click
  on:mouseover
  on:focus
  on:mouseout
  on:blur
  on:mouseenter
  on:mouseleave
>
  <slot />
  <div 
    class='segmented-control-background' 
    role='presentation' 
    style='width: {backgroundLength}px; transform: translateX({backgroundOffset}px)'
  ></div>
</div>