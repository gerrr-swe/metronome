<script lang="ts">
	type Props = {
		href: string;
		iconSrc: string;
		alt: string;
	};

	let { href, iconSrc: src, alt }: Props = $props();
</script>

<a {href} target="_blank" class="icon-link">
	<li>
		<img {src} {alt} width="30" height="30" />
	</li>
</a>

<style>
	.icon-link:hover {
		transform: translate(0, -5px) scale(1.15);
		transition: ease-in-out 0.2s;
	}
	.icon-link {
		transition: ease-in-out 0.2s;
    opacity: 0.8;
	}
</style>
