<script lang="ts">
	import { createWeb3Modal, defaultWagmiConfig } from '@web3modal/wagmi';

	import { mainnet, arbitrum } from 'viem/chains';
	import { reconnect } from '@wagmi/core';

	// 1. Get a project ID at https://cloud.walletconnect.com
	const projectId = 'a12fcd1832839e143ea6cf11b8d62b99';

	// 2. Create wagmiConfig
	const metadata = {
		name: 'verify.box',
		description: 'Do not trust, verify.box.',
		url: 'https://verify.box',
		icons: ['https://avatars.githubusercontent.com/u/37784886']
	};

	const chains = [mainnet, arbitrum] as const;
	export const config = defaultWagmiConfig({
		chains,
		projectId,
		metadata
	});
	reconnect(config);

	// 3. Create modal
	const modal = createWeb3Modal({
		wagmiConfig: config,
		projectId,
		enableAnalytics: true, // Optional - defaults to your Cloud configuration
		enableOnramp: true // Optional - false as default
	});

	function connect() {
		modal.open();
	}

	// import { configureChains, createConfig } from '@wagmi/core';
	// import { mainnet, arbitrum, bsc, optimism, polygon } from '@wagmi/core/chains';
	// import { publicProvider } from '@wagmi/core/providers/public';
	// // import { alchemyProvider } from '@wagmi/core/providers/alchemy';
	// // import { infuraProvider } from '@wagmi/core/providers/infura';
	// import { createModal } from '@rabby-wallet/rabbykit';

	// const { chains, publicClient, webSocketPublicClient } = configureChains(
	// 	[mainnet, arbitrum, bsc, optimism, polygon],
	// 	[
	// 		// alchemyProvider({ apiKey: 'yourAlchemyApiKey' }),
	// 		// infuraProvider({ apiKey: 'yourInfuraApiKey' }),
	// 		publicProvider()
	// 	]
	// );

	// const config = createConfig({
	// 	autoConnect: true,
	// 	publicClient,
	// 	webSocketPublicClient
	// });

	// const rabbyKit = createModal({
	// 	chains,
	// 	wagmi: config,
	// 	projectId: 'a12fcd1832839e143ea6cf11b8d62b99',
	// 	appName: 'verify.box'
	// });

	// function connect() {
	// 	rabbyKit.open();
	// 	console.log('current rabbykit modal open status here:', rabbyKit.getOpenState());
	// }
</script>

<h1>verify<b>.box</b></h1>

<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<button on:click={connect}>Connect</button>
