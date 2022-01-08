<script>
  import { getContext, onMount } from 'svelte'

  export let id = ''
  export let title = ''
  export let disabled = false
  export let controls = ''

  let ref = null
  let length = 0
  let offset = 0

  const ctx = getContext('SegmentedControl')
  const selectedIndex = ctx.selectedIndex
  const index = ctx.setIndex()

  $: selected = $selectedIndex === index
  $: if (selected) { ref?.focus() }
  
  onMount(() => {
    length = Math.round(ref.getBoundingClientRect().width)
    offset = Math.round(ref.getBoundingClientRect().left)
    ctx.addSegment({ index, length, offset })
  })
</script>


<button 
  bind:this={ref}
  id={id !== '' 
    ? id 
    : console.error('Segmented Control -> Segment: Property "id" is empty. Provide a unique non-empty id.')} 
  class='segmented-control-item {selected ? "selected" : ""}'
  role='tab'
  aria-controls={controls}
  aria-selected={selected}
  tabindex={selected ? '0' : '-1'}
  disabled={disabled}
  {...$$restProps}
  on:click
  on:click|preventDefault={() => { 
    if (index !== $selectedIndex) {
      ctx.setAsSelected(index)
    }
    ref.focus()
  }}
  on:mouseover
  on:focus
  on:mouseout
  on:blur
  on:mouseenter
  on:mouseleave
  on:keydown
  on:keydown='{({ key }) => {
    if (key === 'ArrowRight') {
      ctx.setAsSelected(index + 1)
    } else if (key === 'ArrowLeft') {
      ctx.setAsSelected(index - 1)
    }
  }}'
>
  <slot>{title}</slot>
</button>