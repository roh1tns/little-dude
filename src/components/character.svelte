<script>
	import Eye from './eye.svelte';

	let { x = $bindable(), y = $bindable() } = $props();
</script>

<div class="flex w-fit flex-col items-center">
	<div
		class="left-[50vh] top-[50vh] box-border flex w-fit flex-col items-center gap-24 rounded-full border-2 border-black bg-blue-400 p-[2vh]"
	>
		<div class="flex gap-20">
			<Eye bind:x bind:y />
			<Eye bind:x bind:y />
		</div>
	</div>

	<div class="relative flex h-[6vh] w-[5vh] justify-center border-x-2 border-black bg-blue-400">
		<div class="h-[1vh] w-[5vh] bg-blue-800"></div>
	</div>

	<div class="h-[20vh] w-[30vh] rounded-full border-2 border-black bg-blue-400"></div>
</div>
