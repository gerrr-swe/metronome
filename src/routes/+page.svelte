<script>
	import { Button } from "$lib";
	import Slider from "$lib/components/Slider.svelte";

  const minBpm = 20;
  const maxBpm = 218;

  let bpm = $state(20);

  function handleIncrement() {
    if (bpm < maxBpm)
    ++bpm;
  }

  function handleDecrement() {
    if (bpm > minBpm)
    --bpm;
  }
</script>

<div class="main">

  <p class="bpm-label">{bpm} BPM</p>
  <div class="controllers" >
    <Button class="button-controller" onclick={handleDecrement} >
      –
    </Button>
    
    <div class="slider-container">
      <Slider bind:value={bpm} ></Slider>
    </div>

    <Button class="button-controller" onclick={handleIncrement} >
      +
    </Button>
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
</style>
