<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import '../app.css';
	import Header from '$lib/components/Header.svelte';

	let { children } = $props();
</script>

<div class="main">
	<Header />
	<div class="metronome-container">{@render children()}</div>
</div>

<style>
	.main {
		height: 100svh;
		display: flex;
		flex-direction: column;
	}

	.metronome-container {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
</style>