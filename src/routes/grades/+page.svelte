<script lang="ts">
	let grades: Array<{ grade: number; importance: number }> = $state([]);

	let newGrade = { grade: 0, importance: 0 };

	function removeGrade(index: number) {
		grades = grades.filter((_, i) => i !== index);
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

<h1 class="mb-2">Grades</h1>

<div class="text-blue-300">
	<h2 class="mb-2">Weighted Average: {weightedAverage}</h2>
</div>

<div class="mb-4 flex flex-col gap-2 border-y-2 border-stone-600">
	<div class="flex flex-row">
		<div>Grade</div>
		<div>|</div>
		<div>Importance</div>
	</div>
	<hr />
	<div class="flex flex-row gap-2 p-1">
		<input
			class="w-10 rounded-md border-2 border-blue-300"
			type="number"
			bind:value={newGrade.grade}
		/>
		<input
			class="w-10 rounded-md border-2 border-blue-300"
			type="number"
			bind:value={newGrade.importance}
		/>
		<div>|</div>
		<button onclick={() => grades.push(newGrade)}>Add Grade</button>
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
