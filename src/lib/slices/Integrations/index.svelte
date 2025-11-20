<script lang="ts">
	import clsx from 'clsx';

	import IconUmbrella from '~icons/fe/umbrella';
	import IconShield from '~icons/fe/shield';
	import IconDocument from '~icons/fe/document';
	import IconHeart from '~icons/fe/heart-o';

	import type { Content } from '@prismicio/client';
	import { PrismicRichText, PrismicText, type SliceComponentProps } from '@prismicio/svelte';
	import background from './background.jpg';
	import Bounded from '$lib/components/Bounded.svelte';
	import LogoBackground from './LogoBackground.svelte';
	import StylizedLogoMark from './StylizedLogoMark.svelte';

	type Props = SliceComponentProps<Content.IntegrationsSlice>;

	const { slice }: Props = $props();

	const icons = {
		umbrella: IconUmbrella,
		shield: IconShield,
		document: IconDocument,
		heart: IconHeart
	};
</script>

<Bounded
	class="relative overflow-hidden"
	data-slice-type={slice.slice_type}
	data-slice-variation={slice.variation}
>
	<img src={background} alt="" class="absolute inset-0 h-full w-full object-cover" />
	<LogoBackground />

	<div class="relative">
		{#if slice.primary.heading}
			<h2
				class="mx-auto max-w-2xl text-balance bg-linear-to-b from-violet-50 to-violet-300 bg-clip-text py-2 text-center text-2xl font-medium text-transparent md:text-7xl"
			>
				<PrismicText field={slice.primary.heading} />
			</h2>
		{/if}

		<div class="mx-auto mt-6 max-w-md text-balance text-center text-gray-300">
			<PrismicRichText field={slice.primary.body} />
		</div>

		<div class="flex flex-col mt-20 items-center md:flex-row">
			{#each slice.primary.icon as item, index}
				{#if slice.primary.icon}
					{#if index === Math.floor(slice.primary.icon.length / 2)}
						<StylizedLogoMark />
						<div class="signal-line rotate-180"></div>
					{/if}
					<div
						class="pulsing-icon flex aspect-square shrink-0 items-center justify-center rounded-full border border-violet-50/30 bg-violet-50/25 p-3 text-3xl text-violet-100 opacity-40 md:text-3xl lg:text-5xl"
					>
						<svelte:component this={icons[item.icon]} />
					</div>
					{#if index < slice.primary.icon.length - 1}
						<div
							class={clsx(
								'signal-line',
								index >= Math.floor(slice.primary.icon.length / 2) ? 'rotate-180' : 'rotate-0'
							)}
						></div>
					{/if}
				{/if}
			{/each}
		</div>
	</div>
</Bounded>
