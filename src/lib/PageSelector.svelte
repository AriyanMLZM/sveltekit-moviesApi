<script lang="ts">
	import Icon from '@iconify/svelte'

	export let pages
	export let changeIndex
	export let index
	export let length
</script>

<div class="flex-center gap-[10px] p-[1.5rem]">
	<button on:click={() => changeIndex('down')} type="button">
		<Icon
			icon="ooui:next-rtl"
			class="text-white hover:text-primary active:text-primary text-[1.5rem]"
		/>
	</button>
	<div>
		<h2 class="text-[1.2rem] text-white font-bold">{index + 1} / {pages}</h2>
	</div>
	<h2 class="text-[1.2rem] text-white font-bold"> - {length}</h2>
	<button on:click={() => changeIndex('up')} type="button">
		<Icon
			icon="ooui:next-ltr"
			class="text-white hover:text-primary active:text-primary text-[1.5rem]"
		/>
	</button>
</div>
