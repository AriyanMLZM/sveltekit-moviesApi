<script lang="ts">
	import { Image } from './'

	export let creators
	export let role: string
</script>

<div
	class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-[20px] mt-[60px]"
>
	{#each creators as person}
		<div class="flex">
			<div class="w-[100px] h-[120px] rounded-[20px] overflow-hidden">
				<Image
					src={import.meta.env.VITE_TMDB_IMAGE_URL_PROFILE +
						person.profile_path}
					alt={person.name}
				/>
			</div>
			<div class="text-white p-[20px]">
				<h2 class="text-[0.9rem]">{person.name}</h2>
				<h3 class="text-[0.8rem] text-primary">{role}</h3>
			</div>
		</div>
	{/each}
</div>
