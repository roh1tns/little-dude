<script lang="ts">
	let { x = $bindable(), y = $bindable() } = $props();

	let outerDiv = $state<HTMLDivElement | null>(null);
	let innerDiv = $state<HTMLDivElement | null>(null);
	let radius = $state(0);
	let innerRadius = $state(0);

	$effect(() => {
		if (outerDiv) {
			radius = outerDiv.offsetWidth / 2;
		}

		if (innerDiv) {
			innerRadius = innerDiv.offsetWidth / 2;
		}
	});

	const calculateConstrainedPosition = (coordinate: number, isX: boolean) => {
		if (!outerDiv) return 0;

		const rect = outerDiv.getBoundingClientRect();
		const centerX = (rect.left + rect.right) / 2;
		const centerY = (rect.top + rect.bottom) / 2;

		// Calculate the distance from the center
		const dx = x - centerX;
		const dy = y - centerY;
		const distance = Math.sqrt(dx * dx + dy * dy);

		// If distance is within radius, return original coordinate
		// Otherwise, calculate the point on the circle's edge
		if (distance <= radius) {
			return coordinate + radius - innerRadius;
		} else {
			// Calculate the point on the circle's edge
			const angle = Math.atan2(dy, dx);
			return isX
				? centerX + radius * Math.cos(angle) + radius - innerRadius
				: centerY + radius * Math.sin(angle) + radius - innerRadius;
		}
	};

	let posX = $derived(calculateConstrainedPosition(x, true));
	let posY = $derived(calculateConstrainedPosition(y, false));

</script>

<div
	bind:this={outerDiv}
	class="h-[10vh] w-[10vh] overflow-hidden rounded-full border-2 border-black bg-white"
>
	<div
		bind:this={innerDiv}
		class="h-[8vh] w-[8vh] rounded-full border-4 border-gray-400 bg-black"
		style:transform="translate({posX - (outerDiv?.getBoundingClientRect().left || 0) - radius}px, {posY -
			(outerDiv?.getBoundingClientRect().top || 0) -
			radius}px)"
	></div>
</div>
