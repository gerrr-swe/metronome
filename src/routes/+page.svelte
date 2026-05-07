<script lang="ts">
	import { Button, Slider } from '$lib';
	import { onMount } from 'svelte';

	const minBpm = 20;
	const maxBpm = 218;

	// one context per document
	let context: AudioContext;

	let bpm = $state(20);
	let playing = $state(false);
	let interval: NodeJS.Timeout;
	let MINUTE_TO_MILISEC = 60000;
	let intervalTime = $derived( MINUTE_TO_MILISEC / bpm );

	const playSound = () => {
		if (!context) return;

		const osc = context.createOscillator();
		const gain = context.createGain();

		osc.type = "square"
		osc.connect(gain);
		gain.connect(context.destination);

		gain.gain.setValueAtTime(1, context.currentTime);
		gain.gain.exponentialRampToValueAtTime(0.00001, context.currentTime + 0.04);

		osc.start();
		osc.stop(context.currentTime + 0.04);
	};

	function handleIncrement() {
		handleStop();
		if (bpm < maxBpm) ++bpm;
	}

	function handleDecrement() {
		handleStop();
		if (bpm > minBpm) --bpm;
	}

	function handleStart() {
		playing = true;
		if (!context) return;

		const handlePlay = () => {
			if (context.state === 'suspended') {
				context.resume().then(playSound);
			} else {
				playSound();
			}
		};

		handlePlay();
		interval = setInterval(handlePlay, intervalTime);
	}

	function handleStop() {
		if (!context) return;
		context.suspend();
		clearInterval(interval);
		playing = false;
	}

	onMount(() => {
		context = new window.AudioContext();
	});
</script>

<div class="main">
	<p class="bpm-label">{bpm} BPM</p>
	<div class="controllers">
		<Button class="button-controller" onclick={handleDecrement}>–</Button>

		<div class="slider-container">
			<Slider bind:value={bpm} minVal={minBpm} maxVal={maxBpm} onchange={handleStop} ></Slider>
		</div>

		<Button class="button-controller" onclick={handleIncrement}>+</Button>
	</div>
	<div class="controllers">
		<Button class="button-text" onclick={!playing ? handleStart : handleStop}
			>{!playing ? 'Start' : 'Stop'}</Button
		>
	</div>
</div>

<style>
	:global(.button-controller) {
		width: 60px;
		height: 60px;
		font-size: 1.5rem;
		font-weight: bold;
		text-align: center;
	}

	:global(.button-text) {
		width: 120px;
		font-size: 1rem;
		text-align: center;
	}

	.controllers {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}

	.bpm-label {
		text-align: center;
		font-size: 2rem;
		font-weight: bold;
	}

	.slider-container {
		width: 200px;
		margin: 10px;
		display: flex;
		align-items: center;
	}

	.main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 1rem;
	}
</style>
