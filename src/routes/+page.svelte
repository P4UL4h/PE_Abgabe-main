<script>
	import Header from '$lib/components/Header.svelte';

	import { slide } from 'svelte/transition';
	import Pattern1 from '$lib/components/Pattern1.svelte';
	import Pattern2 from '$lib/components/Pattern2.svelte';
	import Pattern3 from '$lib/components/Pattern3.svelte';
	import Pattern4 from '$lib/components/Pattern4.svelte';
	import Pattern5 from '$lib/components/Pattern5.svelte';

	let patterns = [
		{
			name: 'Variante 1',
			component: Pattern1,
			description: 'erster Ansatz ohne Farbe'
		},
		{
			name: 'Variante 2',
			component: Pattern2,
			description: 'Hinzufügen von Farbe'
		},
		{
			name: 'Variante 3',
			component: Pattern3,
			description: 'Nutzung der Zwischenräumen'
		},
		{
			name: 'Variante 4',
			component: Pattern4,
			description: 'Spiel mit Farbe'
		},
		{
			name: 'Muster 2',
			component: Pattern5,
			description: 'gleiche Form anderes Muster'
		},
	];

	let selectedPattern = $state(0);
	let SelectedPattern = $derived(patterns[selectedPattern].component);
</script>

<div class="app-container">
	<Header />
	<main class="app-main">
		<div class="sidebar-left">
			{#each patterns as pattern, index}
				<button
					class="sidebar-left-item"
					class:selected={selectedPattern === index}
					onclick={() => (selectedPattern = index)}
					>{pattern.name}
					{#if selectedPattern === index}
						<div transition:slide class="sidebar-left-description">{pattern.description}</div>
					{/if}
				</button>
			{/each}
		</div>

		<SelectedPattern />
	</main>
</div>
