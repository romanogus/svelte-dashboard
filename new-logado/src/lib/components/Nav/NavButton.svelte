<script lang="ts">
	import Button from '$lib/components/ui/button/button.svelte';
	import { onDestroy } from 'svelte';
	import { isExpanded } from './navbarStore';
	import { fade } from 'svelte/transition';
	import { page } from '$app/stores';

	export let route: string;

	const fadeIn = {
		delay: 0,
		duration: 300
	};

	const fadeOut = {
		delay: 0,
		duration: 300
	};

	let toggleState: boolean;

	const unsubscribe = isExpanded.subscribe((value) => {
		toggleState = value;
	});

	onDestroy(() => {
		unsubscribe();
	});
</script>

<li class="flex justify-center mb-[10px]">
	<Button
		href={route ? route : '#'}
		class={$page.url.pathname === route
			? 'flex flex-row px-0 py-2 w-full h-14 justify-start text-white no-underline border-l-4 border-r-0 rounded-none transition-none border-l-orange-500'
			: 'flex flex-row px-0 py-2 w-full h-14 justify-start text-white no-underline border-l-4 border-r-0 rounded-none transition-none hover:border-l-orange-300 border-l-transparent'}
	>
		<slot name="icon" />
		<!-- Slot visivel se toggleState é true -->
		{#if toggleState}
			<span class="text" in:fade={fadeIn} out:fade={fadeOut}>
				<slot />
			</span>
		{/if}
	</Button>
</li>

<style>
	li {
		margin-bottom: 10px;
	}

	.text {
		font-size: 14px;
		margin-left: 16px;
	}

	li {
		width: 230px;
	}
</style>
