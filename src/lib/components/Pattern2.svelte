<script>
	import chroma from 'chroma-js';
	import Slider from '$lib/ui/Slider.svelte';
	import Toggle from '$lib/ui/Toggle.svelte';

	let squareSize = $state(100);
	let LängeKurz = $state(25);

	let hue = $state(0);
	let color1 = $derived(chroma.oklch(0.5, 0.2, hue).hex());
	let color2 = $derived(chroma.oklch(0.3, 0.2, hue).hex());

	function getColor(xi, yi) {
		if (yi % 2 == 0) {
			if (xi % 2 == 0) {
				return color1;
			} else {
				return color2;
			}
		} else {
			if (xi % 2 == 0) {
				return color2;
			} else {
				return color1;
			}
		}
	}

	let showStroke = $state(false);

</script>

<div class="svg-container">
	<svg viewBox="-500 -500 1000 1000" class="svg-canvas">
		{#each Array(11) as _, yi}
			{#each Array(11) as _, xi}
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) "
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					fill={getColor(xi, yi)}
					stroke={showStroke ? 'white' : 'none'}
				/>
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(90)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					fill={getColor(xi, yi)}
					stroke={showStroke ? 'white' : 'none'}
				/>
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(180)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					fill={getColor(xi, yi)}
					stroke={showStroke ? 'white' : 'none'}
				/>
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(270)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					fill={getColor(xi, yi)}
					stroke={showStroke ? 'white' : 'none'}
				/>

			{/each}
		{/each}
	</svg>
</div>

<div class="sidebar-right">
	<Slider min={100} max={250} bind:value={squareSize} label="Modulgröße" />
	<Slider min={0} max={squareSize / 2} bind:value={LängeKurz} label="Breite" />
	<Slider min={0} max={360} bind:value={hue} label="Farbton" />
	<Toggle bind:value={showStroke} label="Umrandungen" />
</div>

