<script lang="ts">
	export let msg: string
</script>

<section class="w-full h-full flex-col flex-center">
	<img draggable="false" src="error.png" alt="not-found" width="200px" />
	<p class="text-white font-bold text-[1.2rem]">{msg}!</p>
	<button
		class="bg-primary text-[1rem] rounded-[20px] py-[10px] px-[20px] font-bold hover:bg-white hover:text-primary active:bg-white active:text-primary text-white mt-[40px]"
		on:click={() => location.reload()}
		type="button">refresh</button
	>
</section>
