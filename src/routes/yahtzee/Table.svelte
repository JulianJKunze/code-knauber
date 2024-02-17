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
		const points = Array(7).fill('');
		const occurences = getOccurences(eyes);
		points[0] = Math.max(...occurences) >= 3 ? sumOfEyes(eyes) : 0;
		points[1] = Math.max(...occurences) >= 4 ? sumOfEyes(eyes) : 0;
		points[2] = occurences.includes(2) & occurences.includes(3) ? 25 : 0;

		points[5] = Math.max(...occurences) >= 5 ? 50 : 0;
		points[6] = sumOfEyes(eyes);
		return points;
	}

	function getOccurences(eyes) {
		let occurence = Array(6);
		for (let i = 1; i <= 6; i++) {
			occurence[i - 1] = eyes.filter((dieNumber) => dieNumber == i).length;
		}
		return occurence;
	}

	function sumOfEyes(eyes) {
		return eyes.reduce((accumulator, currentValue) => accumulator + currentValue);
	}
</script>

<div class="flex space-x-10">
	<table class="table table-lg text-xl">
		{#each upperSectionLabels as upperSectionLabel, i}
			<tr>
				<td class="border-y p-2 text-left">{upperSectionLabel}</td>
				<td class="border-y p-2 text-right">{upperSectionPoints[i]}</td>
			</tr>
		{/each}
	</table>

	<table class="table table-lg text-xl">
		{#each lowerSectionLabels as lowerSectionLabel, i}
			<tr>
				<td class="border-y p-2 text-left">{lowerSectionLabel}</td>
				<td class="border-y p-2 text-right">{lowerSectionPoints[i]}</td>
			</tr>
		{/each}
	</table>
</div>
