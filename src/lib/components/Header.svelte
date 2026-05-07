<script lang="ts">
	import IconButton from './IconButton.svelte';

	const ICONS: { href: string; icon: string; alt: string }[] = [
		{
			href: 'https://github.com/gerrr-swe',
			icon: 'https://s.magecdn.com/social/mb-github.svg',
			alt: 'github'
		},
		{
			href: 'https://www.linkedin.com/in/gerardo-ramirez-swe',
			icon: 'https://s.magecdn.com/social/mb-linkedin.svg',
			alt: 'linkedin'
		}
  ];
</script>

<header>
	<ul>
		<span class="left side">
			<li><a href="https://rrg44.github.io/portafolio-personal/">Other cool things</a></li>
		</span>
		<span class="right side">
      {#each ICONS as icon (icon)}
        <IconButton
          href={icon.href}
          iconSrc={icon.icon}
          alt={icon.alt}
        />
      {/each}
		</span>
	</ul>
</header>

<style>
	header {
		background-color: var(--primary-bg);
		box-shadow: 0px 5px 10px #aaaaaa;
		padding: 30px;
	}

	ul {
		list-style: none;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		gap: 20px;
	}

	.side {
		display: flex;
		gap: var(--gap);
	}
</style>
