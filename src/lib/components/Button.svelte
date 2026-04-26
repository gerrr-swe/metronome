<script lang="ts">
	import type { Snippet } from "svelte";

  type Props = {
    class?: string;
    onclick?: () => void;
    children: Snippet;
  }

  let { onclick, children, class: className } : Props = $props();
</script>

<button {onclick} class={className} >
  {@render children()}
</button>

<style>
  button {
    background-color: var(--primary-red);
    border: none;
    border-radius: var(--roundness);
    padding: var(--padding);
    color: var(--primary-white);
  }

  button:hover {
    background-color: var(--primary-strong-red);
    transform: scale(1.03,1.03);
  }

  button:active {
    background-color: var(--primary-red);
    transform: scale(1,1);
  }
</style>