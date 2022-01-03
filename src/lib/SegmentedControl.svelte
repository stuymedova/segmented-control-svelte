<script>
  import { setContext } from 'svelte'

  export let selectedIndex = 0

  $: segments = []

  setContext('SegmentedControl', {
    addSegment: ({ id, title, isSelected }) => {
      segments = [...segments, { id, title, isSelected }]
    },
    setAsSelected: (id) => {
      const recentlySelectedIndex = segments.map(({ id }) => id).indexOf(id)
      if(selectedIndex !== recentlySelectedIndex) {
        selectedIndex = recentlySelectedIndex
      }
    }
  })
</script>


<div selectedIndex={selectedIndex}>
  <slot />
</div>