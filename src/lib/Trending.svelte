<script lang="ts">
	import { fly } from 'svelte/transition'
	import { Error, Image, Loader } from './'

	export let type: string

	const getData = async () => {
		const resTmdb = await fetch(
			`https://api.themoviedb.org/3/trending/${type}/week?api_key=${import.meta.env.VITE_TMDB_API_KEY}`
		)
		const { results } = await resTmdb.json()
		results.length = 6
		return results
	}
</script>

<h2 class="mt-[50px] py-[20px] text-[1.2rem] text-center font-bold text-white">
	Trending
</h2>
{#await getData()}
	<Loader />
{:then trendings}
	<section
		in:fly={{ y: 200, duration: 1000 }}
		class="grid grid-cols-3 md:grid-cols-6 gap-[20px] px-[20px] mb-[40px]"
	>
		{#each trendings as trend}
			<a
				href="/{type}/{trend.id}"
				class="flex w-full flex-col gap-[10px] justify-between"
			>
				<div class="w-full min-h-[120px] rounded-[20px] overflow-hidden">
					<Image
						src={import.meta.env.VITE_TMDB_IMAGE_URL_POSTER + trend.poster_path}
						alt={trend.name || trend.title}
					/>
				</div>
				<h2 class="text-[0.9rem] font-bold text-white text-center">
					{trend.name || trend.title}
				</h2>
			</a>
		{/each}
	</section>
{:catch error}
	<Error msg={error.message} />
{/await}
