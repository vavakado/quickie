<script lang="ts">
	let grades: Array<{ grade: number; importance: number }> = $state([]);

	let newGrade: { grade: number | undefined; importance: number | undefined } = $state({
		grade: undefined,
		importance: undefined
	});

	function removeGrade(index: number) {
		grades = grades.filter((_, i) => i !== index);
	}

	function addGrade(newGrade: { grade: number; importance: number }) {
		if (typeof newGrade.grade === 'number' && typeof newGrade.importance === 'number') {
			grades.push(newGrade);
		}
	}

	const countAverage = (grades: Array<{ grade: number; importance: number }>) => {
		let sum = 0;
		let count = 0;
		for (let i = 0; i < grades.length; i++) {
			sum += grades[i].grade * grades[i].importance;
			count += grades[i].importance;
		}
		return sum / count;
	};

	let weightedAverage = $derived(parseFloat(countAverage(grades).toFixed(1)));
</script>

<svetle:head>
	<title>Grades</title>
</svetle:head>

<h1 class="mb-2">Grades</h1>

<div class="text-blue-300">
	<h2 class="mb-2">Weighted Average: {weightedAverage}</h2>
</div>

<div class="mb-4 flex flex-col gap-2 border-y-2 border-stone-600">
	<div class="flex flex-row gap-2 p-1">
		<input
			class="w-20 rounded-md border-2 border-blue-100 p-px"
			type="number"
			placeholder="grade"
			bind:value={newGrade.grade}
		/>
		<input
			class="w-20 rounded-md border-2 border-blue-100 p-px"
			type="number"
			placeholder="importnc."
			bind:value={newGrade.importance}
		/>
		<div>|</div>
		<button
			onclick={() => {
				if (newGrade.grade && newGrade.importance) {
					addGrade(newGrade);
					newGrade = { grade: undefined, importance: undefined };
				}
			}}>Add Grade</button
		>
	</div>
</div>

{#each grades as grade, index}
	<div class="flex flex-row gap-2 rounded-md border-2 border-stone-600 p-1">
		<div>{grade.grade}</div>
		<div>{grade.importance}</div>
		<div>|</div>
		<button class="text-red-400" onclick={() => removeGrade(index)}>Remove Grade</button>
	</div>
{/each}

<style lang="css">
	input[type='number'] {
		-webkit-appearance: textfield;
		-moz-appearance: textfield;
		appearance: textfield;
	}
	input[type='number']::-webkit-inner-spin-button,
	input[type='number']::-webkit-outer-spin-button {
		-webkit-appearance: none;
	}
</style>
