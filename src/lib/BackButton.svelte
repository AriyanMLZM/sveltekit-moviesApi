<script lang="ts">
	import Icon from '@iconify/svelte'
</script>

<div class="w-full h-[60px] flex items-center">
	<button on:click={() => history.back()} type="button">
		<Icon
			icon="ion:arrow-back-outline"
			class="text-white hover:text-primary active:text-primary text-[1.8rem]"
		/>
	</button>
</div>
