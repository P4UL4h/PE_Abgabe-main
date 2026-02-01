<script>
	import chroma from 'chroma-js';
	import Slider from '$lib/ui/Slider.svelte';
	import Toggle from '$lib/ui/Toggle.svelte';

	let squareSize = $state(100);

	let LängeKurz = $state(25);
	const snapValue = 25;
    const snapRange = 0.5;

    $effect(() => {
        if (Math.abs(LängeKurz - snapValue) < snapRange) {
            LängeKurz = snapValue;
        }
    });

	let differentGaps = $state(false);
	let color2AsGaps = $state(false);

	let hue = $state(192);
	let color1 = $derived(chroma.oklch(0.5, 0.2, hue).hex());
	let color2 = $derived(color2AsGaps ? color3 : chroma.oklch(0.3, 0.2, hue).hex());
	let color3 = $derived(chroma.oklch(0.7, 0.2, hue).hex());
	let color4 = $derived(differentGaps ? chroma.oklch(0.9, 0.2, hue).hex() : color3);


	function getColor(xi, yi) {
		if (yi % 2 == 0) {
			if (xi % 2 == 0) {
				return color2;
			} else {
				return color1;
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
		{#each Array(13) as _, yi}
			{#each Array(12) as _, xi}
				<g>
					<polygon
						transform="translate({0 + (xi - 5) * squareSize + (yi % 2) * (-squareSize) * 1.5} {0 + (yi - 5) * squareSize - yi * (squareSize * 0.25)}) "
						points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize /2} {squareSize / 2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
						fill={getColor(xi, yi)}
						stroke={showStroke ? 'white' : 'none'}
					/>
					<polygon
						transform="translate({0 + (xi - 4) * squareSize + (yi % 2) * (-squareSize * 1.5)} {0 + (yi - 5) * squareSize - yi * (squareSize * 0.25)}) rotate(90)"
						points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize /2} {squareSize / 2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
						fill={getColor(xi, yi)}
						stroke={showStroke ? 'white' : 'none'}
					/>
					 <polygon
						transform="translate({0 + (xi - 4) * squareSize + (yi % 2) * (-squareSize * 1.5)} {0 + (yi - 4) * squareSize - yi * (squareSize * 0.25)}) rotate(180)"
						points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize /2} {squareSize / 2}, {squareSize / 2 - LängeKurz} {squareSize / 2 }"
						fill={getColor(xi, yi)}
						stroke={showStroke ? 'white' : 'none'}
					/>
					<polygon
						transform="translate({0 + (xi - 5) * squareSize + (yi % 2) * (-squareSize * 1.5)} {0 + (yi - 4) * squareSize - yi * (squareSize * 0.25)}) rotate(270)"
						points="0 0, {squareSize / 2} {squareSize / 2 - LängeKurz}, {squareSize /2} {squareSize / 2}, {squareSize / 2 - LängeKurz} {squareSize / 2}"
						fill={getColor(xi, yi)}
						stroke={showStroke ? 'white' : 'none'}
					/>
				</g>

			{/each}
		{/each}
	</svg>
</div>

<div class="sidebar-right">
	<Slider min={100} max={250} bind:value={squareSize} label="Modulgröße" />
	<Slider min={0} max={squareSize / 2} step={0.01} bind:value={LängeKurz} label="Breite" />
	<Slider min={0} max={360} bind:value={hue} label="Farbton" />
	<Toggle bind:value={showStroke} label="Umrandungen" />
</div>

