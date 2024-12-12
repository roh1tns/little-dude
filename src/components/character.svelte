<script>
	import Eye from './eye.svelte';

	let { x = $bindable(), y = $bindable() } = $props();
</script>

<div
	class="fixed left-[500px] top-[100px] box-border w-fit bg-blue-400 p-[2rem] rounded-full flex flex-col items-center gap-24"
>
	<div class="flex gap-20">
		<Eye bind:x bind:y />
		<Eye bind:x bind:y />
	</div>
</div>
