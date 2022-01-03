<script>
  import { getContext } from 'svelte'

  export let id = ''
  export let title = ''
  export let isSelected = false
  
  const ctx = getContext('SegmentedControl')

  ctx.addSegment({ id, title, isSelected })
</script>


<button 
  id={id}
  on:click|preventDefault={() => { ctx.setAsSelected(id) }}
>
  <slot />
</button>