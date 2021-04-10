<script>
	import Counter from '$lib/Counter.svelte';
	import { onMount } from 'svelte';

	let Arionum = null;

	onMount(async () => {
		const module = await import('arionum-js');

		Arionum = module.default;
		const arionum = new Arionum();

		arionum.nodeAddress = 'https://node.ariochain.info/';

		await arionum.generateAccount().then(accountDetails => {
			console.log(accountDetails);
		})
	});

</script>

<main>
	<div class="h-screen w-screen bg-gray-100 flex items-center">
		<div class="container flex flex-col md:flex-row items-center justify-center px-5 text-gray-700">
			<div class="max-w-lg text-center">
				<h1 class="text-5xl font-dark font-bold m-6">Hello world!</h1>

				<Counter />

				<p class="m-6">Visit <a href="https://svelte.dev">svelte.dev</a> to learn how to build Svelte apps.</p>
			</div>
		</div>
	</div>
</main>