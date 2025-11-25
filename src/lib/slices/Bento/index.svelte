<script lang="ts">
	import clsx from 'clsx';
	import Bounded from '$lib/components/Bounded.svelte';
	import type { Content } from '@prismicio/client';
	import { PrismicRichText, PrismicText, type SliceComponentProps } from '@prismicio/svelte';
	import GoldText from './GoldText.svelte';
	import Heading2 from '$lib/components/Heading2.svelte';

	type Props = SliceComponentProps<Content.BentoSlice>;

	const { slice }: Props = $props();
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	{#if slice.primary.heading}
		<PrismicRichText
			field={slice.primary.heading}
			components={{ em: GoldText, heading2: Heading2 }}
		/>
	{/if}
	{#if slice.primary.body}
		<div class="mx-auto mt-6 max-w-3xl text-balance text-center text-gray-300">
			<PrismicRichText field={slice.primary.body} />
		</div>
	{/if}
	{#if slice.primary.bento}
		<div class="grid mt-16 max-w-4xl grid-rows-[auto_auto_auto] gap-8 md:grid-cols-3 md:gap-10">
			{#each slice.primary.bento as item}
				<div
					class={clsx(
						'grid glass-container row-span-3 grid-rows-subgrid gap-4 rounded-lg bg-gray-950/60 p-4 before:bg-gray-100/10',
						item.wide ? 'md:col-span-2' : 'md:col-span-1'
					)}
				>
					<h3 class="text-2xl"><PrismicText field={item.title} /></h3>
					<div class="max-w-lg text-balance text-gray-300">
						<PrismicRichText field={item.body} />
					</div>
				</div>
			{/each}
		</div>
	{/if}
</Bounded>
