<script lang="ts">
	export let src: string
	export let alt: string
	let loading = true
	let imageError = false
</script>

<div
	class={`w-full h-full flex-center bg-white/20 ${loading ? ' animate-pulse' : ''}`}
>
	{#if !imageError}
		<img
			{src}
			{alt}
			class="w-full h-full object-cover"
			on:load={() => (loading = false)}
			on:error={() => {
				loading = false
				imageError = true
			}}
		/>
	{:else}
		<h1 class="text-[1.5rem] text-[#111] font-bold">403</h1>
	{/if}
</div>
