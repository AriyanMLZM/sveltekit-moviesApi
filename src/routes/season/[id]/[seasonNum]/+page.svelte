<script lang="ts">
	import { Error, Loader, EpisodesList, BackButton } from '$lib'
	import type { IApiEpisodes } from '../../../../types/index.svelte'
	import { page } from '$app/state'

	const getData = async () => {
		const resTmdb = await fetch(
			`https://api.themoviedb.org/3/tv/${page.params.id}/season/${page.params.seasonNum}?api_key=${import.meta.env.VITE_TMDB_API_KEY}`
		)
		const {
			episodes,
			poster_path: poster,
			name,
		} = (await resTmdb.json()) as IApiEpisodes

		return {
			episodes,
			poster,
			name,
		}
	}
</script>

{#await getData()}
	<Loader />
{:then season}
	<section
		class="w-full h-full bg-center bg-cover"
		style:background-image="url({import.meta.env.VITE_TMDB_IMAGE_URL +
			season.poster})"
	>
		<div
			class="page-scroll w-full h-full bg-black/80 backdrop-blur-[3px] overflow-y-auto px-[20px] pb-[60px]"
		>
			<BackButton />
			<div class="text-white flex-center p-[20px] gap-[20px]">
				<h2 class=" text-[1.5rem]">{season.name}</h2>
			</div>
			<EpisodesList episodes={season.episodes} />
		</div>
	</section>
{:catch error}
	<Error msg={error.message} />
{/await}
