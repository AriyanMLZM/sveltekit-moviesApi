<script lang="ts">
	import { Image } from './'
	export let item
	export let type
</script>

<a
	href="/{type}/{item.id}"
	class="bg-black/50 hover:bg-white/30 active:bg-white/30 rounded-[20px] w-full flex justify-between flex-col hover:text-black active:text-black text-white"
>
	<div class="w-full h-full min-h-[120px] rounded-t-[20px] overflow-hidden">
		<Image
			src={import.meta.env.VITE_TMDB_IMAGE_URL_POSTER + item.poster}
			alt={item.title}
		/>
	</div>
	<div class="w-full px-[0.7rem] py-[10px] select-none">
		<h1
			class="text-[0.9rem] font-bold text-left w-full overflow-hidden overflow-ellipsis text-nowrap"
		>
			{item.title}
		</h1>
		<div
			class="w-full flex items-center justify-between mt-[10px] text-[0.8rem]"
		>
			<h2>tmdb - {item.rate}</h2>
			<h2>{item.date}</h2>
		</div>
	</div>
</a>
