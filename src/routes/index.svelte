<script>
	import '$lib/lightMode.css'
  import { SegmentedControl, Segment } from '$lib'
</script>


<div class='segmented-control-container'>
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

  .segmented-control-container {
		width: 100%;
		position: absolute;
		left: 0;
		top: 12px;
		display: flex;
		justify-content: center;
  }

  :global(.segmented-control-item) {
    outline: none;
  }
</style>