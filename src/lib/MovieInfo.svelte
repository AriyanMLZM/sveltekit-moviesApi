<script lang="ts">
	import { fly } from 'svelte/transition'
	import type { IMovie } from '../types/index.svelte'
	import { Image } from './'

	export let movie: IMovie
</script>

<div
	in:fly={{ y: 100, duration: 1000 }}
	class="w-full flex justify-center gap-[40px] items-center flex-col md:justify-normal md:items-start md:flex-row"
>
	<div class="w-[300px] h-[300px] rounded-[20px] overflow-hidden">
		<Image
			src={import.meta.env.VITE_TMDB_IMAGE_URL_BACKGROUND +
				movie.backgroundImage}
			alt={movie.title}
		/>
	</div>
	<div class="text-white">
		<h1 class="text-[2rem] font-bold">{movie.title}</h1>
		{#each movie.genres as genre, index}
			<span class="text-[0.8rem] text-primary">{genre.name}</span>
			{#if index !== movie.genres.length - 1}
				<span class="text-[0.8rem]">- {' '}</span>
			{/if}
		{/each}
		<h2 class="text-[0.85rem] mt-[20px] w-[250px] flex justify-between">
			<span class="text-primary">Release</span>
			{movie.releaseDate}
		</h2>
		<h2 class="text-[0.85rem] mt-[20px] w-[250px] flex justify-between">
			<span class="text-primary">Language</span>
			{movie.language}
		</h2>
		<h2 class="text-[0.85rem] mt-[20px] w-[250px] flex justify-between">
			<span class="text-primary">Runtime</span>
			{movie.runtime} mins
		</h2>
		<h2 class="text-[0.85rem] mt-[20px] w-[250px] flex justify-between">
			<span class="text-primary">Tmdb</span>
			{movie.vote}
		</h2>
	</div>
	<div class="p-[10px] md:p-[50px]">
		<h2 class="text-white text-[1.1rem]">" {movie.tagline} "</h2>
	</div>
</div>
<div class="p-[20px] mt-[20px]">
	<p class="text-white text-[0.9rem] text-justify">
		{movie.overview}
	</p>
</div>
