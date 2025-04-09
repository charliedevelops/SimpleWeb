<script lang="ts">
	import '../app.css';
	import { cn } from '$lib/utils';
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';
	let { children } = $props();

	let loaded = $state(false);
	onMount(() => {
		loaded = true;
	});
</script>

<div class="min-h-screen bg-gradient-to-b from-charlie-dark to-black bg-radial-gradient dark">
	<!-- Navbar with centered navigation -->
	<header
		class="fixed top-0 left-0 right-0 z-40 bg-black/30 backdrop-blur-md border-b border-white/5"
	>
		<div class="container relative flex items-center h-16 px-4 sm:px-6 mx-auto">
			<!-- Logo section on the left -->
			<div class="flex items-center gap-2">
				<img src="/logo.png" alt="Simple Start Logo" class="h-8" />
			</div>

			<!-- Navigation links - absolutely positioned and centered -->
			<nav
				class="hidden md:flex absolute left-1/2 top-1/2 transform -translate-x-1/2 -translate-y-1/2 items-center gap-6"
			>
				<a href="#features" class="text-white/70 hover:text-white transition-colors">Features</a>
				<a href="#screenshots" class="text-white/70 hover:text-white transition-colors"
					>Screenshots</a
				>
				<a
					href="https://github.com/charliedesigns/Simple-Start"
					class="text-white/70 hover:text-white transition-colors">GitHub</a
				>
			</nav>

			<!-- Download button on the right -->
			<div class="ml-auto flex items-center gap-4">
				<a
					href="https://github.com/charliedesigns/Simple-Start"
					class="charlie-button-primary text-sm px-4 py-2"
					target="_blank"
					rel="noopener noreferrer"
				>
					Download
				</a>
			</div>
		</div>
	</header>

	<!-- Main content with padding for navbar -->
	<main class="pt-16">
		{#if loaded}
			<div in:fade={{ duration: 500, delay: 200 }}>
				{@render children()}
			</div>
		{:else}
			<div class="min-h-screen flex items-center justify-center">
				<div
					class="w-12 h-12 rounded-full border-4 border-t-charlie-blue border-r-charlie-red border-b-charlie-yellow border-l-charlie-green animate-spin"
				></div>
			</div>
		{/if}
	</main>
</div>
