<script>
	import { PrismicLink } from '@prismicio/svelte';
	import WordMark from './WordMark.svelte';

	let { settings } = $props();
</script>

<footer>
	<nav
		class="flex flex-col items-center justify-between gap-6 border-t border-x-gray-600 px-8 py-7 md:flex-row"
		aria-label="Footer"
	>
		<a href="/">
			<WordMark />
			<span class="sr-only">{settings.data.site_title} home page</span>
		</a>
		<!-- <ul>
			{#each settings.data.navigation as item}
				<li>
					<PrismicLink field={item.link} class="inline-flex min-h-11 items-center">
						{item.link.text}
					</PrismicLink>
				</li>
			{/each}
		</ul> -->
	</nav>
</footer>
