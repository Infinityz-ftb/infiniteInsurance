<script lang="ts">
	import { PrismicImage, PrismicText, SliceZone } from '@prismicio/svelte';

	import { components } from '$lib/slices';
	import type { PageProps } from '../$types';
	import Bounded from '$lib/components/Bounded.svelte';
	import TriangleGrid from '$lib/components/TriangleGrid.svelte';

	const { data }: PageProps = $props();
</script>

<Bounded>
	<div class="relative grid w-full place-items-center text-center">
		<TriangleGrid />

		<h1 class="text-5xl md:text-7xl font-medium">
			<PrismicText field={data.page.data.company} />
			<span class="block text-lg text-yellow-500">Case Study</span>
		</h1>
		<p class="mb-4 mt-8 max-w-xl text-lg text-slate-300">
			<PrismicText field={data.page.data.description} />
		</p>
		<PrismicImage field={data.page.data.image} class="rounded-lg " />
	</div>
	<div class="mx-auto md:mt-12 mt-8">
		<SliceZone slices={data.page.data.slices} {components} />
	</div>
</Bounded>
