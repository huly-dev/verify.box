<script lang="ts">
	import { configureChains, createConfig } from '@wagmi/core';
	import { mainnet, arbitrum, bsc, optimism, polygon } from '@wagmi/core/chains';
	import { publicProvider } from '@wagmi/core/providers/public';
	// import { alchemyProvider } from '@wagmi/core/providers/alchemy';
	// import { infuraProvider } from '@wagmi/core/providers/infura';
	import { createModal } from '@rabby-wallet/rabbykit';

	const { chains, publicClient, webSocketPublicClient } = configureChains(
		[mainnet, arbitrum, bsc, optimism, polygon],
		[
			// alchemyProvider({ apiKey: 'yourAlchemyApiKey' }),
			// infuraProvider({ apiKey: 'yourInfuraApiKey' }),
			publicProvider()
		]
	);

	const config = createConfig({
		autoConnect: true,
		publicClient,
		webSocketPublicClient
	});

	const rabbyKit = createModal({
		chains,
		wagmi: config,
		projectId: 'a12fcd1832839e143ea6cf11b8d62b99',
		appName: 'verify.box'
	});

	function connect() {
		rabbyKit.open();
		console.log('current rabbykit modal open status here:', rabbyKit.getOpenState());
	}

	chains.forEach((chain) => {
		console.log('chain:', chain);
	});
</script>

<h1>verify<b>.box</b></h1>

<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<button on:click={connect}>Connect</button>
