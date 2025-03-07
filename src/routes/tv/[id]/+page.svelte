<script lang="ts">
	import { page } from '$app/state'
	import {
		Error,
		Loader,
		TvInfo,
		Creators,
		Seasons,
		CastList,
		Networks,
		BackButton,
	} from '$lib'
	import type { IApiTv } from '../../../types/index.svelte'

	let docTitle = 'Loading...'

	const getData = async () => {
		const resTmdb = await fetch(
			`https://api.themoviedb.org/3/tv/${page.params.id}?api_key=${import.meta.env.VITE_TMDB_API_KEY}`
		)
		const {
			name: title,
			last_air_date: lastAir,
			first_air_date: firstAir,
			poster_path: poster,
			vote_average: vote,
			backdrop_path: backgroundImage,
			genres,
			original_language: language,
			overview,
			tagline,
			created_by: creators,
			number_of_episodes: episodesNum,
			number_of_seasons: seasonsNum,
			seasons,
			status,
			networks,
		} = (await resTmdb.json()) as IApiTv

		docTitle = title
		return {
			title,
			poster,
			vote,
			backgroundImage,
			genres,
			language,
			overview,
			tagline,
			lastAir,
			firstAir,
			creators,
			episodesNum,
			seasonsNum,
			seasons,
			status,
			networks,
		}
	}

	const getCast = async () => {
		const resTmdb = await fetch(
			`https://api.themoviedb.org/3/tv/${page.params.id}/credits?api_key=${import.meta.env.VITE_TMDB_API_KEY}`
		)
		const { cast } = await resTmdb.json()
		return cast
	}
</script>

<svelte:head>
	<title>{docTitle}</title>
</svelte:head>

{#await getData()}
	<Loader />
{:then tv}
	<section
		class="w-full h-full bg-center bg-cover"
		style:background-image="url({import.meta.env
			.VITE_TMDB_IMAGE_URL_BACKGROUND + tv.backgroundImage})"
	>
		<div
			class="page-scroll w-full h-full bg-black/80 backdrop-blur-[3px] overflow-y-auto px-[20px] pb-[60px]"
		>
			<BackButton />
			<TvInfo {tv} />
			<Seasons seasons={tv.seasons} id={page.params.id} />
			<Networks networks={tv.networks} />
			<Creators creators={tv.creators} role="Creator" />
			{#await getCast()}
				<Loader />
			{:then cast}
				<CastList {cast} />
			{:catch error}
				<Error msg={error.message} />
			{/await}
		</div>
	</section>
{:catch error}
	<Error msg={error.message} />
{/await}
