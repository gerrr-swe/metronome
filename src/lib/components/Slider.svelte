<script lang="ts">
  type Props = {
    value: number;
    minVal: number;
    maxVal: number;
    onchange: () => void;
  }

  let  { value = $bindable(), minVal, maxVal, onchange } : Props = $props();
</script>

<input {onchange} type="range" class="generator-input" min={minVal} max={maxVal} bind:value />

<style>
	/* Target Input */
.generator-input {
  -webkit-appearance: none;
  width: 100%;
  background: transparent;
  cursor: pointer;
}

/* --- Webkit Browsers --- */
.generator-input::-webkit-slider-runnable-track {
  height: 4px;
  background: #909090;
  border-radius: 2px;
  border: 0px solid #cbd5e1;
  box-shadow: 0px 2px 0px rgba(0, 0, 0, 0.1);
}

.generator-input::-webkit-slider-thumb {
  -webkit-appearance: none;
  height: 26px;
  width: 26px;
  background: #f03861;
  border-radius: 30px;
  border: 0px solid #464646;
  box-shadow: 0px 4px 0px rgba(240, 56, 97, 0);
  margin-top: -11px;
}

/* --- Firefox --- */
.generator-input::-moz-range-track {
  height: 4px;
  background: #909090;
  border-radius: 2px;
  border: 0px solid #cbd5e1;
  box-shadow: 0px 2px 0px rgba(0, 0, 0, 0.1);
}

.generator-input::-moz-range-thumb {
  height: 26px;
  width: 26px;
  background: #f03861;
  border-radius: 30px;
  border: 0px solid #464646;
  box-shadow: 0px 4px 0px rgba(240, 56, 97, 0);
}
</style>
