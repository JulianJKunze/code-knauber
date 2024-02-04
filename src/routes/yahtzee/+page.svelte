<script>
	import Die from './Die.svelte';
	import Table from './Table.svelte';

	const infiniteRollsPossible = false;

	const eyes = [0, 0, 0, 0, 0];
	const diceIds = [0, 1, 2, 3, 4];
	let isKept = [false, false, false, false, false];
	let lastRoll = 0;
	$: canSelectDies = lastRoll === 1 || lastRoll === 2;

	const rollMessage = ['Roll the dice!', 'Second roll!', 'Last roll!', 'Select category'];

	function rollDies() {
		for (const dieId of diceIds) {
			if (!isKept[dieId]) {
				eyes[dieId] = Math.ceil(Math.random() * 6);
			}
		}
		infiniteRollsPossible ? (lastRoll = 1) : (lastRoll = lastRoll + 1);
		if (lastRoll === 3) {
			isKept = [true, true, true, true, true];
		}
	}

	function toggleDieState(dieId) {
		if (canSelectDies) {
			isKept[dieId] = !isKept[dieId];
		}
	}
</script>

<main class="flex justify-center">
	<div class="flex flex-col space-y-5 j w-144">
		<h1 class="text-center text-3xl text-bold">Let's play Yahtzee</h1>
		<button class="btn btn-lg btn-primary" disabled={lastRoll === 3} on:click={rollDies}>
			{rollMessage[lastRoll]}</button
		>

		<div class="flex h-24 space-x-5 justify-between content-center">
			{#if lastRoll !== 0}
				{#each diceIds as dieId}
					<Die
						eyes={eyes[dieId]}
						isKept={isKept[dieId]}
						canSelectDie={canSelectDies}
						on:dieClicked={() => toggleDieState(dieId)}
					></Die>
				{/each}
			{/if}
		</div>

		<div>
			<Table {eyes}></Table>
		</div>
	</div>
</main>
