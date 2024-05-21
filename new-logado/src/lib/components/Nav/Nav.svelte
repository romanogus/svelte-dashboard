<script lang="ts">
	import {
		ArrowLeftRightIcon,
		HomeIcon,
		PanelLeftClose,
		PanelRightClose,
		SearchIcon,
		UserRoundCogIcon
	} from 'lucide-svelte';
	import NavButton from './NavButton.svelte';
	import Navlogo from './NavLogo.svelte';
	import { isExpanded } from './navbarStore';
	import Button from '$lib/components/ui/button/button.svelte';
	import { onDestroy } from 'svelte';
	import { page } from '$app/stores';

	let color = 'none';

	function toggleNavbar() {
		isExpanded.update((state) => !state);
	}

  function hideNavbar() {
    isExpanded.set(false);
  }

	function handleHover() {
		color = 'orange';
		console.log(color);
	}

	function handleOut() {
		color = 'transparent';
		console.log(color);
	}

	//subscribing to isExpanded store
	let expanded: boolean;
	const unsubscribe = isExpanded.subscribe((value) => {
		expanded = value;
	});

	onDestroy(() => {
		unsubscribe();
	});
</script>

<nav
	class="flex flex-col items-center w-16 bg-asset-blue h-dvh justify-items-center justify-between rounded-r-[26px]"
	class:expanded
>
	<ul class="w-full transition-none">
		<Navlogo />
		<!-- <Button>
			<SearchIcon size="24" class="ml-4" />
			Buscar
		</Button> -->
		<NavButton route="/home">
			<HomeIcon size="24" slot="icon" class="ml-4"/>
			Home
		</NavButton>
		<NavButton route="/movimentacoes">
			<ArrowLeftRightIcon size="24" slot="icon" class="ml-4" />
			Movimentações
		</NavButton>
	</ul>

	<ul class="w-full">
		<Button
			variant="outline"
			size="icon"
			class={expanded
				? 'justify-end bg-transparent outline-none border-none w-full hover:bg-inherit pr-4'
				: 'justify-center bg-transparent outline-none border-none w-full hover:bg-inherit'}
			on:click={toggleNavbar}
			on:mouseenter={handleHover}
			on:mouseleave={handleOut}
		>
    {#if expanded}
      <PanelLeftClose size="24" color="white" fill={color} />
      {:else}
      <PanelRightClose size="24" color="white" fill={color} />
    {/if}
		</Button>
		<NavButton route="/conta">
			<UserRoundCogIcon size="24" slot="icon" class="ml-4" />
			Conta
		</NavButton>
	</ul>
</nav>

<style>
	nav {
		grid-area: nav;
		width: 64px;
		height: 100vh;
		transition: width ease-out 200ms;
		overflow: hidden;
	}

	.expanded {
		transition: width ease-out 200ms;
		width: 230px;
	}

	ul {
		list-style-type: none;
		padding: 0;
		margin: 0;
	}
</style>
