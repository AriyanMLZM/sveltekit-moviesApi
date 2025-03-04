<script lang="ts">
	import { fly } from 'svelte/transition'
	export let data
	export let type
	import { Item } from './'
</script>

<section
	in:fly={{ y: 200, duration: 1000 }}
	class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-[1.2rem] pt-[30px] px-[20px] pb-[50px]"
>
	{#each data as item}
		<Item {item} {type} />
	{/each}
</section>
