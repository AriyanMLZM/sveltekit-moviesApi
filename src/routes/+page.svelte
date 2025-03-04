<script lang="ts">
	import movies from '../constants/tmdb-ids.movies.json'
	import { List, Error, Loader, Trending, PageSelector } from '$lib'
	import type { IApiMovie } from '../types/index.svelte'

	const packSize = 20
	const length = movies.length
	const pages = Math.ceil(length / packSize)
	let index = 0

	$: gettingMovies = getData(index)

	const changeIndex = (action: string) => {
		switch (action) {
			case 'up':
				index = index === pages - 1 ? 0 : index + 1
				break
			case 'down':
				index = index === 0 ? pages - 1 : index - 1
				break
		}
	}

	const getData = async (index: number) => {
		let data = []
		const start = index * 20
		const end = index === pages - 1 ? length : (index + 1) * 20
		for (let i = start; i < end; i++) {
			const resTmdb = await fetch(
				`https://api.themoviedb.org/3/movie/${movies[i].id}?api_key=${import.meta.env.VITE_TMDB_API_KEY}`
			)
			const {
				title: title,
				release_date: date,
				poster_path: poster,
				vote_average: vote,
			} = (await resTmdb.json()) as IApiMovie

			data.push({
				id: movies[i].id,
				title,
				date: date.split('-')[0],
				poster,
				rate: vote.toFixed(1),
			})
		}
		return data
	}
</script>

<svelte:head>
	<title>Movotopia | Movie</title>
</svelte:head>

<Trending type="movie" />
<PageSelector {pages} {changeIndex} {index} {length} />
{#await gettingMovies}
	<Loader />
{:then moviesData}
	<List data={moviesData} type={'movie'} />
{:catch error}
	<Error msg={error.message} />
{/await}
<PageSelector {pages} {changeIndex} {index} {length} />
