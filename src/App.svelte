<script>
	import Chapter from './Chapter.svelte'
	import chapters from './chapters.js'

	let current_chapter = 0;

	function handleMove(event) {
		current_chapter = event.detail;
	}
</script>

<main>
	<Chapter text="{chapters[current_chapter]}" on:move="{handleMove}"/>
</main>

<style>
	main {
		text-align: center;
		margin: 0;
		padding: 0;
		height: 100%;
		background-color: black;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>