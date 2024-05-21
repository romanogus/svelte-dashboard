<script>
	import '../app.css';
	import Nav from '../lib/components/Nav/Nav.svelte';
	import Profile from '../lib/components/Profile/Profile.svelte';

</script>

<div class="app">
	<Nav />
	<main class="main container">
		<Profile />
		<slot />
	</main>
</div>

<style>
	.app {
		display: flex;
		flex-direction: row;
		height: 100vh;
	}
</style>
