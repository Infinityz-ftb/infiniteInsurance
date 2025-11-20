<script>
	import clsx from 'clsx';
	import IconClose from '~icons/ph/x-bold';
	import IconLMenu from '~icons/ph/list-bold';
	import { PrismicLink } from '@prismicio/svelte';
	import WordMark from './WordMark.svelte';
	import ButtonLink from './ButtonLink.svelte';
	import { asLink } from '@prismicio/client';
	import { page } from '$app/stores';

	/** @type {import('@prismicio/client').Content.SettingsDocument} */
	export let settings;

	let isOpen = false;
	const toggleOpen = () => (isOpen = !isOpen);
	const close = () => (isOpen = false);

	/** @param {import('@prismicio/client').LinkField} link */
	const isActive = (link) => {
		const path = asLink(link);

		return path && $page.url.pathname.includes(path);
	};
</script>

<header class="p-4 md:p-6">
	<nav
		class="mx-auto max-w-6xl flex flex-col py-2 justify-between font font-medium text-white md:flex-row md:items-center"
		aria-label="main"
	>
		<div class="flex items-center justify-between">
			<a href="/" onclick={close} class="z-50">
				<WordMark />
				<span class="sr-only">{settings.data.site_title} home page</span>
			</a>
			<button
				type="button"
				class="block p-2 text-3xl text-white md:hidden cursor-pointer"
				aria-expanded={isOpen}
				onclick={toggleOpen}><IconLMenu /></button
			>
		</div>

		<!-- Mobile Nav -->
		<div
			class={clsx(
				'fixed inset-0 z-40 flex flex-col items-end bg-gray-950 pr-4 pt-6 transition-transform duration-300 ease-in-out md:hidden',
				isOpen ? 'translate-x-0' : 'translate-x-full'
			)}
		>
			<button
				type="button"
				class="block p-2 text-3xl text-white md:hidden cursor-pointer"
				aria-expanded={isOpen}
				onclick={close}
			>
				<IconClose />
			</button>
			<ul class="grid justify-items-end gap-8">
				{#each settings.data.navigation as item}
					<li>
						{#if item.cta_button}
							<ButtonLink
								onclick={close}
								field={item.link}
								aria-current={isActive(item.link) ? 'page' : undefined}
								>{item.link.text}
							</ButtonLink>
						{:else}
							<PrismicLink
								onclick={close}
								field={item.link}
								class="min-h-11 block text-3xl first:mt-8 px-3"
								aria-current={isActive(item.link) ? 'page' : undefined}
							>
								{item.link.text}
							</PrismicLink>
						{/if}
					</li>
				{/each}
			</ul>
		</div>

		<!-- Desktop Nav -->
		<ul class="hidden md:flex gap-6">
			{#each settings.data.navigation as item}
				<li>
					{#if item.cta_button}
						<ButtonLink
							onclick={close}
							field={item.link}
							aria-current={isActive(item.link) ? 'page' : undefined}
						>
							{item.link.text}
						</ButtonLink>
					{:else}
						<PrismicLink
							field={item.link}
							class="inline-flex min-h-11 items-center"
							aria-current={isActive(item.link) ? 'page' : undefined}
						>
							{item.link.text}
						</PrismicLink>
					{/if}
				</li>
			{/each}
		</ul>
	</nav>
</header>
