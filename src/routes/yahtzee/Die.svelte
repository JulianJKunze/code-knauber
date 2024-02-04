<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->

<script>
	import { createEventDispatcher } from 'svelte';
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
	const dieSvgStrings = [die1, die2, die3, die4, die5, die6];
</script>

<div
	on:click={() => dispatch('dieClicked')}
	class="shrink w-24 border-4 rounded-3xl
  		{canSelectDie ? 'cursor-pointer' : ''}
  		{isKept ? 'border-primary' : 'border-transparent'}"
>
	{@html dieSvgStrings[eyes - 1]}
</div>
