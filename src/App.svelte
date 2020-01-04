<script>
	import Chapter from './Chapter.svelte'
	import chapters from './chapters.js'

	let story;

	const json = localStorage.getItem("story");
	if (json) {
		story = JSON.parse(json);
	} else {
		story = [0];
	}

	let current_chapter = story[story.length-1];

	function handleMove(event) {
		current_chapter = event.detail;
		story.push(+current_chapter);
		localStorage.setItem("story", JSON.stringify(story));
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