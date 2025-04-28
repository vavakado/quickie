<script lang="ts">
	import '../app.css';

	let { children } = $props();
</script>

<div class="flex min-h-screen flex-col justify-between p-8 sm:p-20">
	<main class="flex flex-grow flex-col items-center justify-center">
		{@render children()}
	</main>
	<footer class="mt-8 text-center text-sm text-gray-500">
		<a class="hover:underline" href="https://github.com/vavakado/quickie" target="_blank"
			>View on Github</a
		>
	</footer>
</div>
