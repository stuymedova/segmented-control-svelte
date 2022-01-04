<script>
  import { setContext } from 'svelte'

  export let selectedIndex = 0

  let segments = []
  let currentIndex = -1
  let backgroundWidth = 0
  let backgroundOffset = 0
  
  setContext('SegmentedControl', {
    setIndex: () => {
      currentIndex += 1
      return currentIndex
    },
    addSegment: ({ id, index, title, isSelected, width, offset }) => {
      if(index === selectedIndex) {
        backgroundWidth = width
        backgroundOffset = offset
      }
      segments = [...segments, { id, index, title, isSelected, width, offset }]
    },
    setAsSelected: (index, width, offset) => {
      if(index !== selectedIndex) {
        selectedIndex = index
        backgroundWidth = width
        backgroundOffset = offset
      }
    }
  })
</script>


<div selectedIndex={selectedIndex}>
  <slot />
  <div style='width: {backgroundWidth}px; transform: translateX({backgroundOffset}px)'></div>
</div>