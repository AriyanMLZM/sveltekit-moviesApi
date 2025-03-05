<script lang="ts">
	import tvs from '../../constants/tmdb-ids.series.json'
	import { List, Error, Trending, PageSelector, Loader } from '$lib'

	const packSize = 20
	const length = tvs.length
	const pages = Math.ceil(length / packSize)
	let index = 0

	$: gettingTvs = getData(index)

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
				`https://api.themoviedb.org/3/tv/${tvs[i].id}?api_key=${import.meta.env.VITE_TMDB_API_KEY}`
			)
			const {
				name: title,
				first_air_date: date,
				poster_path: poster,
				vote_average: vote,
			} = await resTmdb.json()

			data.push({
				id: tvs[i].id,
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
	<title>Movotopia | Tv</title>
</svelte:head>

<Trending type="tv" />
<PageSelector {pages} {changeIndex} {index} {length} />
{#await gettingTvs}
	<Loader />
{:then tvsData}
	<List data={tvsData} type={'tv'} />
{:catch error}
	<Error msg={error.message} />
{/await}
<PageSelector {pages} {changeIndex} {index} {length} />
