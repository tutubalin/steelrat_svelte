<script context="module">
    import chapters from './chapters.js'
</script>

<script>

    import { createEventDispatcher } from 'svelte';

    export let number;
    export let active;

    let text;

    $: text = chapters[number];

    const eventDispatcher = createEventDispatcher();

    function handleClick(chapter) {
        eventDispatcher('move', chapter);
    }
</script>

<div class:passive="{!active}">
    {#each text.split("\n") as line}
        <p>
        {#each line.split(/#(\d+)/) as chunk, index}
            {#if active && (index&1)}
                <button on:click="{handleClick(chunk)}">{chunk}</button>
            {:else}
                {chunk}
            {/if}
        {/each}
        </p>
    {/each}
</div>

<style>

    .passive {
        opacity: 0.4;
    }

    button {
        margin: 0;
        padding: 0 1em 0 1em;
        background-color: #aaaaff;
        border-color: #444480;
        border-radius: 7px;
    }

    p {
        padding: 0px 10px 0px 10px;
        margin: 2pt;
        /* margin-top: 0;
        margin-bottom: 0; */
        
    }

    div {
        font-size: 10pt;
        text-align: justify;
        border: 2px solid #cccccc;
        background-color: #e8e8e8;
        width: 50%;
        margin: auto;
        margin-top: 5pt;
        margin-bottom: auto;
        /* display: table-cell;
        vertical-align: center; */
        border-radius: 4pt;
    }
</style>