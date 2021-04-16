<script context="module" lang="ts">
	let current: HTMLAudioElement;
</script>

<script lang="ts">
	export let author: string = '紫咲シオン';
	export let content: string;
	export let cite: string;
	export let date: string;
	export let src: string;

	let audio: HTMLAudioElement;
	let paused = true;

	function stopOthers() {
		// Disable for now
		// Ideally we should seek to the start first before unpausing.
		// using current.load() to stop others doesn't work for subsequent play.
		// if (current && current !== audio) {
		// 	current.pause();
		// }
		current = audio;
	}

	function playPause() {
		if (paused) {
			audio.play();
		} else {
			audio.pause();
		}
	}
</script>

<figure on:click={playPause}>
	<blockquote {cite}>
		<h2>{content}</h2>
	</blockquote>
	<!-- svelte-ignore a11y-media-has-caption -->
	<audio bind:this={audio} bind:paused on:play={stopOthers} {src} />
	<figcaption>—{author}, {date}. <cite><a href={cite}>Twitter</a></cite>.</figcaption>
</figure>

<style>
	figure {
		text-align: left;
		border-left: 3px solid rgb(214, 193, 217);
		padding: 2em;
		margin-bottom: 2em;
		border-bottom-right-radius: 1em;
	}

	figure:focus,
	figure:hover {
		border-top: 2px solid rgb(214, 193, 217);
		border-left: 5px solid rgb(214, 193, 217);
		cursor: pointer;
	}

	figure:active {
		background-color: rgba(214, 193, 217, 0.2);
	}

	blockquote {
		color: rgb(237, 186, 132);
		margin: 0;
	}

	a {
		color: rgb(160, 86, 103);
	}
</style>
