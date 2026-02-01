<script>
	import Slider from '$lib/ui/Slider.svelte';
	import Toggle from '$lib/ui/Toggle.svelte';

	let squareSize = $state(100);
	let LängeKurz = $state(25);

	let offset = $state(0);

</script>

<div class="svg-container">
	<svg viewBox="-500 -500 1000 1000" class="svg-canvas">
		{#each Array(11) as _, yi}
			{#each Array(11) as _, xi}
				<polygon
					transform="translate({0 + (xi - 5) * (squareSize + offset)} {0 + (yi - 5) * (squareSize + offset)}) "
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					stroke='white'
				/>
				<polygon
					transform="translate({0 + (xi - 5) * (squareSize + offset)} {0 + (yi - 5) * (squareSize + offset)}) rotate(90)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					stroke='white'
				/>
				<polygon
					transform="translate({0 + (xi - 5) * (squareSize + offset)} {0 + (yi - 5) * (squareSize + offset)}) rotate(180)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					stroke='white'
				/>
				<polygon
					transform="translate({0 + (xi - 5) * (squareSize + offset)} {0 + (yi - 5) * (squareSize + offset)}) rotate(270)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					stroke='white'
				/>
			{/each}
		{/each}
	</svg>
</div>

<div class="sidebar-right">
	<Slider min={100} max={250} bind:value={squareSize} label="Modulgröße" />
	<Slider min={0} max={squareSize / 2} bind:value={LängeKurz} label="Breite" />
	<Slider min={0} max={squareSize} bind:value={offset} label="Abstand" />
</div>