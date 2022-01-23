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
    length = Math.round(ref.clientWidth)
    offset = Math.round(ref.offsetLeft)
    ctx.addSegment({ index, disabled, length, offset })
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
  aria-disabled={disabled}
  aria-selected={selected}
  tabindex={selected ? '0' : '-1'}
  {...$$restProps}
  on:click
  on:click|preventDefault={() => { 
    if (index !== $selectedIndex && disabled !== true) {
      ctx.setAsSelected(index)
    }
    ref.focus()
  }}
  on:click
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


<style>
  .segmented-control-item {
    position: relative;
    box-sizing: border-box;
    width: 75px;
    margin: 0;
    padding: 12px;
    border: 0;
    border-radius: 14px;
    z-index: 2;

    font-family: sans-serif;
    font-size: 14px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    
    transition: color 275ms;
    background-color: rgba(255, 255, 255, 0);
    outline: none;
    cursor: pointer;
  }

  .segmented-control-item.selected {
    color: rgb(0, 125, 255);
    pointer-events: none;
  }

  .segmented-control-item[aria-disabled = true] {
    color: rgb(145, 145, 150);
    pointer-events: none;
  }
</style>