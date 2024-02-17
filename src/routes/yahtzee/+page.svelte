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

<div class="flex justify-center">
	<div class="flex max-w-screen-md grow flex-col space-y-8">
		<h1 class="text-bold text-center text-3xl">Let's play Yahtzee !</h1>
		<button class="btn btn-primary btn-lg" disabled={lastRoll === 3} on:click={rollDies}>
			{rollMessage[lastRoll]}</button
		>

		<div class="flex grow content-center justify-between space-x-6">
			{#each diceIds as dieId}
				<Die
					eyes={eyes[dieId]}
					isKept={isKept[dieId]}
					canSelectDie={canSelectDies}
					on:dieClicked={() => toggleDieState(dieId)}
				></Die>
			{/each}
		</div>

		<div>
			<Table {eyes}></Table>
		</div>
	</div>
</div>
