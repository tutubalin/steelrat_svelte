<script>
	import Chapter from './Chapter.svelte';
	import { afterUpdate } from 'svelte';

	let story;

	const json = localStorage.getItem("story");
	if (json) {
		story = JSON.parse(json);
	} else {
		story = [0];
	}

	let currentChapter = story[story.length-1];

	let div;
	let autoScroll = false;

	afterUpdate(() => {
		if (autoScroll) {
			div.scrollTo(0, div.scrollHeight);
			autoScroll = false;
		}
	});

	function handleMove(event) {
		currentChapter = event.detail;
		story = [...story, +currentChapter];
		localStorage.setItem("story", JSON.stringify(story));
		autoScroll = true;
	}

	function resetStory(event) {
		story = [0];
		localStorage.setItem("story", JSON.stringify(story));
		currentChapter = 0;
	}

</script>

<main>
	<div class="navigation">
		<button on:click="{resetStory}">Начать сначала</button>
	</div>
	<div bind:this="{div}">
		{#each story as chapter}
		<Chapter number="{chapter}" active="{chapter==currentChapter}" on:move="{handleMove}"/>
		{/each}
	</div>
</main>

<style>

	.navigation {
		position: sticky;
		top: 1em;
		left: 1em;
		text-align: left;
	}

	.navigation > button {
		margin: 1em;
		left: 1em;
	}


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