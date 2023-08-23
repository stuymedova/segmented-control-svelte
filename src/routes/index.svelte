<script>
	import '$lib/main.css'
  import { SegmentedControl, Segment } from '$lib'
</script>


<div class='component-wrapper'>
  <SegmentedControl>
    <Segment>First</Segment>
    <Segment>Second</Segment>
  </SegmentedControl>
</div>


<style>
  :global(body) {
    width: 100%;
    height: auto;
    margin: 0;
    padding: 0;
    background-color: rgb(255, 255, 255);
  }

  .component-wrapper {
		width: 100%;
		position: absolute;
		left: 0;
		top: 12px;
		display: flex;
		justify-content: center;
  }
</style>