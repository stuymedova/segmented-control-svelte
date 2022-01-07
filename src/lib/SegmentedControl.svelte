<script>
  import { setContext } from 'svelte'
  import { writable } from 'svelte/store'

  export let selectedIndex = writable(0)

  let segments = []
  let currentIndex = -1
  let backgroundWidth = 0
  let backgroundOffset = 0
  
  setContext('SegmentedControl', {
    selectedIndex,
    setIndex: () => {
      currentIndex += 1
      return currentIndex
    },
    addSegment: ({ index, width, offset }) => {
      if (index === $selectedIndex) {
        backgroundWidth = width
        backgroundOffset = offset
      }
      segments = [...segments, { index, width, offset }]
    },
    setAsSelected: (index) => {
      if (index !== $selectedIndex) {
        $selectedIndex = index
        backgroundWidth = segments[$selectedIndex].width
        backgroundOffset = segments[$selectedIndex].offset
      }
    },
    setNeighbourAsSelected: (displacement) => {
      $selectedIndex += displacement

      if ($selectedIndex < 0) {
        $selectedIndex = 0
      } else if ($selectedIndex >= segments.length) {
        $selectedIndex = segments.length - 1
      }

      backgroundWidth = segments[$selectedIndex].width
      backgroundOffset = segments[$selectedIndex].offset
    }
  })
</script>


<div 
  class='segmented-control' 
  role='tablist'
  aria-orientation='horizontal'
  selectedIndex={$selectedIndex}
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
    style='width: {backgroundWidth}px; transform: translateX({backgroundOffset}px)'
  ></div>
</div>