<script lang="ts">
	import clsx from 'clsx';
	import Bounded from '$lib/components/Bounded.svelte';
	import type { Content } from '@prismicio/client';
	import { isFilled } from '@prismicio/client';
	import {
		PrismicImage,
		PrismicLink,
		PrismicRichText,
		PrismicText,
		type SliceComponentProps
	} from '@prismicio/svelte';

	type Props = SliceComponentProps<Content.CaseStudiesSlice>;

	const { slice }: Props = $props();
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	{#if slice.primary.heading}
		<h2 class="max-w-2xl text-balance text-center text-5xl font-medium md:text-7xl">
			<PrismicText field={slice.primary.heading} />
		</h2>
	{/if}
	{#if slice.primary.body}
		<div class="mx-auto text-balance mt-6 max-w-md text-center text-gray-300">
			<PrismicRichText field={slice.primary.body} />
		</div>
	{/if}
	<div class="mt-20 grid gap-16">
		{#each slice.primary.case_study as item, index}
			<div
				class="relative group grid gap-4 opacity-85 transition-opacity duration-300 hover:cursor-pointer hover:opacity-100 md:grid-cols-2 md:gap-8 lg:grid-cols-3"
			>
				{#if isFilled.contentRelationship(item.case_study)}
					<div class="flex col-span-1 flex-col justify-center gap-4">
						<h3 class="text-4xl">
							<PrismicText field={item.case_study.data?.company} />
						</h3>
						<div class="max-w-md">
							<PrismicRichText field={item.case_study.data?.description} />
						</div>
						<PrismicLink
							document={item.case_study}
							class="z-1 after:absolute after:inset- hover:underline"
						>
							Read <PrismicText field={item.case_study.data?.company} /> Case Study
						</PrismicLink>
					</div>
					<div class={clsx('relative lg:col-span-2', index % 2 && 'md:-order-1')}>
						<div
							class="image-glow bg-white-500 -bottom-8 -left-4 absolute h-1/2 w-1/2 rounded-full opacity-0 mix-blend-screen blur-3xl transition-opacity duration-500 group-hover:opacity-30"
						></div>
						<div
							class="image-glow bg-blue-500 -right-4 -top-8 absolute h-1/2 w-1/2 rounded-full opacity-0 mix-blend-screen blur-3xl transition-opacity duration-500 group-hover:opacity-30"
						></div>
						<PrismicImage
							field={item.case_study.data?.image}
							sizes="(max-width: 768px) 100vw, 50vw"
							class="z-20 scale-[.98] rounded-xl transition-transform duration-300 group-hover:scale-100"
						/>
					</div>
				{/if}
			</div>
		{/each}
	</div>
</Bounded>
