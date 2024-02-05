<script>
	export let eyes;

	$: upperSectionPoints = calculateUpperSectionPoints(eyes);
	$: lowerSectionPoints = calculateLowerSectionPoints(eyes);

	const upperSectionLabels = ['Aces', 'Twos', 'Threes', 'Fours', 'Fives', 'Sixes'];

	const lowerSectionLabels = [
		'Three Of A Kind',
		'Four Of A Kind',
		'Full House',
		'Small Straight',
		'Large Straight',
		'Yahtzee',
		'Chance'
	];

	function calculateUpperSectionPoints(eyes) {
		let points = [];
		for (let categoryNumber = 1; categoryNumber <= 6; categoryNumber++) {
			points[categoryNumber - 1] =
				eyes.filter((dieNumber) => dieNumber == categoryNumber).length * categoryNumber;
		}
		return points;
	}

	function calculateLowerSectionPoints(eyes) {
		return Array(7).fill(0);
	}
</script>

<div class="flex space-x-10">
	<table class="table table-lg text-xl">
		{#each upperSectionLabels as upperSectionLabel, i}
			<tr>
				<td class=" border-y p-2 text-left">{upperSectionLabel}</td>
				<td class=" border-y p-2 text-right">{upperSectionPoints[i]}</td>
			</tr>
		{/each}
	</table>

	<table class="table table-lg text-xl">
		{#each lowerSectionLabels as lowerSectionLabel, i}
			<tr>
				<td class=" border-y p-2 text-left">{lowerSectionLabel}</td>
				<td class=" border-y p-2 text-right">{lowerSectionPoints[i]}</td>
			</tr>
		{/each}
	</table>
</div>
