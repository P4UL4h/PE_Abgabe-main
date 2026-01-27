<script>
	import chroma from 'chroma-js';
	import Slider from '$lib/ui/Slider.svelte';
	import Toggle from '$lib/ui/Toggle.svelte';

	let squareSize = $state(100);
	let LängeKurz = $state(25);
	console.log(squareSize);

	// let differentGaps = $state(false);
	// let color2AsGaps = $state(false);

	let offset = $state(65);
	let offset2 = $state(0);
	let offset3 = $state(90);
	let offset4 = $state(0);

	let hue = $state(0);
	let color1 = $derived(chroma.oklch(0.5, 0.2, hue).hex());
	let color2 = $derived(chroma.oklch(0.3, 0.2, hue).hex());
	// let color3 = $derived(chroma.oklch(0.7, 0.2, hue).hex());
	// let color4 = $derived(differentGaps ? chroma.oklch(0.9, 0.2, hue).hex() : color3);

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

	let showStroke = $state(true);

</script>

<div class="svg-container">
	<svg viewBox="-500 -500 1000 1000" class="svg-canvas">
		{#each Array(11) as _, yi}
			{#each Array(11) as _, xi}
				<!-- unten rechts -->
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

				<!-- Zwischenraum-Rauten -->
				<!-- rechts -->
				<!-- <polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize})"
					points="0 0, {squareSize / 2} {-squareSize / 2 + LängeKurz}, {squareSize} 0, {squareSize /
						2} {squareSize / 2 - LängeKurz}"
					fill={getColor(xi, yi)}
				/> -->
				<!-- unten -->
				<!-- <polygon
					transform="translate({0 + (xi - 5) * squareSize} {0 + (yi - 5) * squareSize}) rotate(90)"
					points="0 0, {squareSize / 2} {-squareSize / 2 + LängeKurz}, {squareSize} 0, {squareSize /
						2} {squareSize / 2 - LängeKurz}"
					fill={getColor(xi, yi)}
				/> -->
			{/each}
		{/each}
	</svg>
</div>

<div class="sidebar-right">
	<Slider min={100} max={250} bind:value={squareSize} label="Modulgröße" />
	<Slider min={0} max={squareSize / 2} bind:value={LängeKurz} label="Breite" />
	<Slider min={0} max={360} bind:value={hue} label="Farbton" />
	<Toggle bind:value={showStroke} label="Umrandungen" />
	<!-- <Toggle bind:value={differentGaps} label="Unterschiedliche Zwischenraumfarben" />
	<Toggle bind:value={color2AsGaps} label="Visuelle Lücken" /> -->
</div>

<!-- <div class="ui">
	<div class="control">
		<input type="range" min="100" max="250" bind:value={squareSize} />
		<label> Modulgröße verändern: {squareSize} </label>
	</div>

	<div class="control">
		<input type="range" min="0" max={squareSize /2} bind:value={LängeKurz} />
		<label> Breite verändern: {LängeKurz} </label>
	</div>

	<div class="control">
		<input type="range" min="0" max="" bind:value={hue} />
		<label> Farbe wählen: {hue} </label>
	</div>

	<div class="control">
		<input type="checkbox" bind:checked={differentGaps} />
		<label> unterschiedliche Zwischenraumfarben: {hue} </label>
	</div>

	<div class="control">
		<input type="checkbox" bind:checked={color2AsGaps} />
		<label> visuelle Lücken: {hue} </label>
	</div>

</div> -->
