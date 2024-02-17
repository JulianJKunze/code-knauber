<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->

<script>
	import { createEventDispatcher } from 'svelte';
	import die0 from '$lib/assets/die0.svg?raw';
	import die1 from '$lib/assets/die1.svg?raw';
	import die2 from '$lib/assets/die2.svg?raw';
	import die3 from '$lib/assets/die3.svg?raw';
	import die4 from '$lib/assets/die4.svg?raw';
	import die5 from '$lib/assets/die5.svg?raw';
	import die6 from '$lib/assets/die6.svg?raw';

	const dispatch = createEventDispatcher();

	export let eyes;
	export let isKept;
	export let canSelectDie;
	const dieSvgStrings = [die0, die1, die2, die3, die4, die5, die6];
</script>

<!-- TODO: Nicer border when selected -->
<div
	on:click={() => dispatch('dieClicked')}
	class="spaxe-x-2 flex-grow rounded-[8px]
		{eyes == 0 ? 'text-neutral' : ''}
  		{canSelectDie ? 'cursor-pointer' : ''} 
  		{isKept ? 'bg-primary bg-opacity-30' : ''}"
>
	{@html dieSvgStrings[eyes]}
</div>
