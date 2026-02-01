<script>
	import chroma from 'chroma-js';
	import Slider from '$lib/ui/Slider.svelte';
	import Toggle from '$lib/ui/Toggle.svelte';

	let squareSize = $state(100);
	let LängeKurz = $state(25);

	let differentGaps = $state(false);
	let color2AsGaps = $state(false);

	let hue = $state(147);
	let color1 = $derived(chroma.oklch(0.5, 0.9, hue).hex());
	let color2 = $derived(color2AsGaps ? color3 : chroma.oklch(0.3, 0.3, (hue + 180) % 360).hex());
	let color3 = $derived(chroma.oklch(0.7, 0.1, (hue + 140)).hex());
	let color4 = $derived(differentGaps ? chroma.oklch(0.6, 0.2, (hue + 120)).hex() : color3);

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
				/>
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(90)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					fill={getColor(xi, yi)}
				/>
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(180)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					fill={getColor(xi, yi)}
				/>
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(270)"
					points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize / 2} {squareSize /
						2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
					fill={getColor(xi, yi)}
				/>

				<!-- Zwischenraumrauten -->
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize})"
					points="0 0, {squareSize / 2} {-squareSize / 2 + LängeKurz}, {squareSize} 0, {squareSize /
						2} {squareSize / 2 - LängeKurz}"
					fill={color3}
				/>
				<polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(90)"
					points="0 0, {squareSize / 2} {-squareSize / 2 + LängeKurz}, {squareSize} 0, {squareSize /
						2} {squareSize / 2 - LängeKurz}"
					fill={color4}
				/>
			{/each}
		{/each}
	</svg>
</div>

<div class="sidebar-right">
	<Slider min={100} max={250} bind:value={squareSize} label="Modulgröße" />
	<Slider min={0} max={squareSize / 2} bind:value={LängeKurz} label="Breite" />
	<Slider min={0} max={360} bind:value={hue} label="Farben" />
	<Toggle bind:value={differentGaps} label="Unterschiedliche Zwischenraumfarben" />
	<Toggle bind:value={color2AsGaps} label="Visuelle Lücken" />
</div>

