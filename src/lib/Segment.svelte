<script>
  import { getContext, onMount } from 'svelte'

  export let label = 'Label'
  export let isDisabled = false

  let ref = null
  let length = 0
  let offset = 0

  const context = getContext('SegmentedControl')
  const orientation = context.orientation
  const index = context.setIndex()
  const focusedSegmentIndex = context.focusedSegmentIndex
  const selectedSegmentIndex = context.selectedSegmentIndex
  
  $: isFocused = $focusedSegmentIndex === index
  $: if (isFocused) { ref?.focus() }
  $: isSelected = $selectedSegmentIndex === index
  
  onMount(() => {
    if (orientation === 'horizontal') {
      length = Math.round(ref.clientWidth) 
      offset = Math.round(ref.offsetLeft) 
    } else if (orientation === 'vertical') {
      length = Math.round(ref.clientHeight) 
      offset = Math.round(ref.offsetTop) 
    }
    
    context.addSegment({ index, isDisabled, length, offset })
  })
</script>


<button 
  bind:this={ref}
  class='segmented-control-item'
  type='button'
  role='tab'
  aria-selected={isSelected}
  aria-disabled={isDisabled}
  tabindex={isSelected ? '0' : '-1'}
  {...$$restProps}
  on:click
  on:click|preventDefault={() => { 
    if (index !== $selectedSegmentIndex && !isDisabled) {
      context.setSelected(index)
    }
  }}
  on:mouseover
  on:focus
  on:mouseout
  on:blur
  on:mouseenter
  on:mouseleave
  on:keydown
  on:keydown='{({ key }) => {
    if (orientation === 'horizontal' && key === 'ArrowRight' || 
        orientation === 'vertical' && key === 'ArrowDown') {
      context.setSelected(index + 1)
    } else if (
        orientation === 'horizontal' && key === 'ArrowLeft' || 
        orientation === 'vertical' && key === 'ArrowUp') {
      context.setSelected(index - 1)
    }
  }}'
>
  <slot>{label}</slot>
</button>