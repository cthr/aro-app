<script>
	import { Arionum } from '$lib/aro-js/arionum';
	import { Transaction } from '$lib/aro-js/transaction';
	import { onMount } from 'svelte';

	let wallet = undefined;

	onMount(async () => {
		const arionum = new Arionum();

		arionum.nodeAddress = 'http://aro-api.herokuapp.com';

		await arionum.generateAccount().then(accountDetails => {
			wallet = {
				"privKey": accountDetails.data.private_key,
				"pubKey": accountDetails.data.public_key,
				"address": accountDetails.data.address
			}
			console.log(wallet.address);
		})
	});

</script>

<main>
	<div class="h-screen w-screen bg-gray-100 flex items-center">
		<div class="container flex flex-col md:flex-row items-center justify-center px-5 text-gray-700">
			<div class="text-center">
				<h1 class="text-5xl font-dark font-bold m-6">Arionum Wallet</h1>

				{#if wallet}
					<p class="text-small mt-6">Address</p>
					<p class="text-xs break-words">{wallet.address}</p>

					<p class="text-small mt-6">Private Key</p>
					<p class="text-xs break-words">{wallet.privKey}</p>
				{/if}
			</div>
		</div>
	</div>
</main>