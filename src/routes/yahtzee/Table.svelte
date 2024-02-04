<script>
	export let eyes;

	$: upperSectionPoints = calculateUpperSectionPoints(eyes);
	const upperSectionLabels = ['Aces', 'Twos', 'Threes', 'Fours', 'Fives', 'Sixes'];

	function calculateUpperSectionPoints(eyes) {
		let points = [];
		for (let categoryNumber = 1; categoryNumber <= 6; categoryNumber++) {
			points[categoryNumber - 1] =
				eyes.filter((dieNumber) => dieNumber == categoryNumber).length * categoryNumber;
		}
		return points;
	}
</script>

<table class="table table-lg text-xl">
	{#each upperSectionLabels as upperSectionLabel, i}
		<tr>
			<th class="p-2 border w-1/2">{upperSectionLabel}</th>
			<td class="p-2 border w-1/2">{upperSectionPoints[i]}</td>
		</tr>
	{/each}
</table>
