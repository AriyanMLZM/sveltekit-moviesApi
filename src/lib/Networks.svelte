<script lang="ts">
	import type { INetwork } from '../types/index.svelte'
	export let networks: INetwork[]
</script>

<section
	class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-[20px] mt-[60px]"
>
	{#each networks as network}
		<div
			class="w-[200px] flex-center bg-white/20 text-white text-[0.8rem] p-[20px] rounded-[20px]"
		>
			{#if network.logo_path}
				<img
					src={import.meta.env.VITE_TMDB_IMAGE_URL_LOGO + network.logo_path}
					alt={network.name}
					class="w-full"
				/>
			{/if}
		</div>
	{/each}
</section>
