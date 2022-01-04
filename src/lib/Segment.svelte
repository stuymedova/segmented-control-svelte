<script>
  import { getContext, onMount } from 'svelte'

  export let id = ''
  export let index = 0
  export let title = ''
  export let isSelected = false
  export let width = 0
  export let offset = 0
  
  let ref = null
  const ctx = getContext('SegmentedControl')
  
  onMount(() => {
    index = ctx.setIndex()
    width = ref.getBoundingClientRect().width
    offset = ref.getBoundingClientRect().left
    ctx.addSegment({ id, index, title, isSelected, width, offset })
  })
</script>


<button 
  bind:this={ref}
  id={id}
  on:click|preventDefault={() => { ctx.setAsSelected(index, width, offset) }}
>
  <slot />
</button>