<script lang="ts">
	import '../app.css'
	import { Navbar } from '$lib'
	let { children } = $props()
</script>

<Navbar />
<main class="w-full h-screen overflow-y-auto list-scroll">
	{@render children()}
</main>

<style>
	main {
		background: linear-gradient(
			45deg,
			rgb(19, 19, 19) 38%,
			rgba(254, 87, 2, 1) 100%
		);
	}
</style>
