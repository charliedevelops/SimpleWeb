<script>
	import { Button } from '$lib/components/ui/button';
	import { Card } from '$lib/components/ui/card';
	import { Modal } from '$lib/components/ui/modal';
	import { cn } from '$lib/utils';
	import { fly, scale, fade } from 'svelte/transition';
	import { onMount } from 'svelte';

	const appScreenshot = '/screen.png';
	const downloadLink = 'https://github.com/charliedesigns/Simple-Start';
	const demoLink = 'https://www.youtube.com/watch?v=z7rgQdmPYnE';

	const featureImages = [
		{
			src: '/screen.png',
			alt: 'Add multiple local servers',
			title: 'Multiple Servers',
			category: 'Creation',
			color: 'charlie-blue'
		},
		{
			src: '/started.png',
			alt: 'Simple interactions with server',
			title: 'Start / Stop',
			category: 'Starting',
			color: 'charlie-yellow'
		},
		{
			src: '/add.png',
			alt: 'Add and customise server without prior experience',
			title: 'Server Configuration',
			category: 'Configuration',
			color: 'charlie-green'
		},
		{
			src: '/config.png',
			alt: 'Advanced custom options ensure it works for whatever workflow via JSON',
			title: 'Advanced configuration',
			category: 'Advanced',
			color: 'charlie-red'
		}
	];

	let mounted = $state(false);

	onMount(() => {
		mounted = true;
	});

	function getStaggerDelay(index, baseDelay = 200) {
		return baseDelay + index * 100;
	}

	function getTagClasses(color) {
		const baseClasses = 'text-sm px-3 py-1 rounded-full border bg-black/30 backdrop-blur-sm';

		switch (color) {
			case 'charlie-blue':
				return `${baseClasses} text-charlie-blue border-charlie-blue/30`;
			case 'charlie-yellow':
				return `${baseClasses} text-charlie-yellow border-charlie-yellow/30`;
			case 'charlie-green':
				return `${baseClasses} text-charlie-green border-charlie-green/30`;
			case 'charlie-red':
				return `${baseClasses} text-charlie-red border-charlie-red/30`;
			default:
				return `${baseClasses} text-white border-white/30`;
		}
	}

	let activeImage = $state(null);
	let modalOpen = $state(false);

	function openImageModal(image) {
		activeImage = image;
		modalOpen = true;
	}

	function closeModal() {
		modalOpen = false;
	}

	onMount(() => {
		window.addEventListener('modalClose', closeModal);

		return () => {
			window.removeEventListener('modalClose', closeModal);
		};
	});

	const sectionsIds = {
		features: 'features',
		screenshots: 'screenshots'
	};
</script>

<div class="container px-4 sm:px-6 pb-16 max-w-6xl mx-auto">
	<!-- Hero Section with animation -->
	{#if mounted}
		<section class="text-center flex flex-col items-center pb-12 pt-16">
			<div in:fly={{ y: 20, duration: 500, delay: 300 }}>
				<div class="flex justify-center mb-6">
					<img src="/icon.png" alt="Simple Start Icon" class="h-28 w-28" />
				</div>
				<h1 class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl font-bold mb-6">
					Simplify boring server tasks with <span class="text-charlie-yellow">Simple Start!</span>
				</h1>
			</div>

			<div in:fly={{ y: 20, duration: 500, delay: 500 }}>
				<p class="text-xl md:text-2xl text-white/80 max-w-3xl">
					Simple start makes it easy for anyone to start up or stop web servers.
				</p>
			</div>

			<div
				class="flex flex-col sm:flex-row gap-4 mt-8"
				in:fly={{ y: 20, duration: 500, delay: 700 }}
			>
				<a
					href={downloadLink}
					class="charlie-button-secondary hover:scale-[1.05] transition-transform relative overflow-hidden group"
				>
					<span class="relative z-10">Download</span>
					<div
						class="absolute inset-0 bg-charlie-yellow/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
					></div>
				</a>
				<a
					href={demoLink}
					class="charlie-button-primary hover:scale-[1.05] transition-transform relative overflow-hidden group"
				>
					<span class="relative z-10">Watch Demo</span>
					<div
						class="absolute inset-0 bg-charlie-blue/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
					></div>
				</a>
			</div>
		</section>

		<!-- Feature Showcase with animation -->
		<section
			id={sectionsIds.features}
			class="my-12 pt-16 -mt-16"
			in:fly={{ y: 20, duration: 500, delay: 900 }}
		>
			<div
				class="backdrop-blur-sm bg-black/50 rounded-3xl border border-white/5 hover:border-white/20 hover:shadow-lg hover:shadow-charlie-blue/10 transition-all duration-300 ease-in-out p-6 sm:p-10"
			>
				<h2 class="text-2xl sm:text-3xl font-semibold mb-6">Key Features</h2>

				<ul class="space-y-4 text-lg">
					<li class="flex gap-3 items-start" in:fly={{ x: -20, duration: 500, delay: 1000 }}>
						<span class="text-charlie-blue mt-1">●</span>
						<span>Easy onboarding for adding servers with optional JSON configuration</span>
					</li>
					<li class="flex gap-3 items-start" in:fly={{ x: -20, duration: 500, delay: 1100 }}>
						<span class="text-charlie-yellow mt-1">●</span>
						<span>Run any command on your local website with a single click</span>
					</li>
					<li class="flex gap-3 items-start" in:fly={{ x: -20, duration: 500, delay: 1200 }}>
						<span class="text-charlie-green mt-1">●</span>
						<span>User-friendly interface for developers of all skill levels</span>
					</li>
					<li class="flex gap-3 items-start" in:fly={{ x: -20, duration: 500, delay: 1300 }}>
						<span class="text-charlie-red mt-1">●</span>
						<span>Automatic server monitoring and status tracking</span>
					</li>
				</ul>
			</div>
		</section>

		<section
			id={sectionsIds.screenshots}
			class="my-16 pt-16 -mt-16"
			in:fly={{ y: 20, duration: 500, delay: 1400 }}
		>
			<h2 class="text-2xl sm:text-3xl font-semibold mb-8">Screenshots</h2>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-6">
				{#each featureImages as image, i}
					<button
						type="button"
						class="project-card overflow-hidden group text-left"
						in:fly={{ y: 20, duration: 500, delay: getStaggerDelay(i, 1500) }}
						onclick={() => openImageModal(image)}
						aria-label={`View ${image.title} screenshot in full size`}
					>
						<div class="relative h-[400px] overflow-hidden rounded-xl group">
							<img
								src={image.src}
								alt={image.alt}
								class="object-cover w-full h-full transition-transform duration-700 group-hover:scale-105"
							/>
							<div
								class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"
							></div>

							<!-- Expand icon -->
							<div
								class="absolute bottom-4 right-4 bg-black/50 backdrop-blur-sm text-white p-2 rounded-full border border-white/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
							>
								<svg
									xmlns="http://www.w3.org/2000/svg"
									width="20"
									height="20"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<polyline points="15 3 21 3 21 9"></polyline>
									<polyline points="9 21 3 21 3 15"></polyline>
									<line x1="21" y1="3" x2="14" y2="10"></line>
									<line x1="3" y1="21" x2="10" y2="14"></line>
								</svg>
							</div>
						</div>
						<div class="mt-4 flex justify-between items-start">
							<div>
								<h3 class="text-xl text-white font-semibold">{image.title}</h3>
								<p class="text-white/70 text-sm">{image.alt}</p>
							</div>
							<span class={getTagClasses(image.color)}>
								{image.category}
							</span>
						</div>
					</button>
				{/each}
			</div>
		</section>

		<section class="mt-16 text-center" in:fly={{ y: 20, duration: 500, delay: 2200 }}>
			<Card
				class="charlie-card p-8 sm:p-10 max-w-3xl mx-auto hover:scale-[1.02] transition-transform duration-300"
			>
				<div class="absolute inset-0 bg-radial-gradient opacity-30 rounded-3xl"></div>
				<div class="relative z-10">
					<h2 class="text-2xl sm:text-3xl font-semibold mb-4">
						Ready to streamline your development workflow?
					</h2>
					<p class="text-white/70 text-lg mb-6">
						Simple Start helps you manage your development servers with ease. Download now and focus
						on coding instead of server management.
					</p>
					<div class="flex flex-col sm:flex-row justify-center gap-4">
						<a
							href={downloadLink}
							class="charlie-button-secondary hover:scale-[1.05] transition-transform relative overflow-hidden group"
						>
							<span class="relative z-10">Get Started Now</span>
							<div
								class="absolute inset-0 bg-charlie-yellow/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
							></div>
						</a>
					</div>
				</div>
			</Card>
		</section>

    <footer
      class="flex flex-col items-center justify-center mt-16 pt-8 border-t border-white/10"
      in:fly={{ y: 20, duration: 500, delay: 2400 }}
    >
      <div class="flex flex-row items-center gap-5">
        <div class="relative group">
          <img src="/icon.png" alt="Simple Start" class="w-16 h-16" />
          <div
            class="absolute inset-0 bg-charlie-blue/20 rounded-full blur-xl opacity-0 group-hover:opacity-100 transition-opacity duration-300 -z-10"
          ></div>
        </div>
        <div>
          <img src="/logo.svg" alt="Simple Start Logo" class="h-16 w-auto" />
        </div>
      </div>
      <p class="mt-4 text-white/60 text-sm">2025 Charlie Fox. All rights reserved.</p>
    </footer>

		<!-- Modal for fullscreen image view -->
		<Modal bind:open={modalOpen} className="flex items-center justify-center">
			{#if activeImage}
				<div class="relative">
					<img
						src={activeImage.src}
						alt={activeImage.alt}
						class="max-h-[85vh] object-contain rounded-lg shadow-2xl max-w-[85vw]"
					/>
					<div
						class="absolute bottom-4 left-4 bg-black/60 backdrop-blur-sm px-4 py-2 rounded-lg text-white border border-white/10"
					>
						<h3 id="modal-title" class="font-medium">{activeImage.title}</h3>
						<p class="text-sm text-white/70">{activeImage.alt}</p>
					</div>
				</div>
			{/if}
		</Modal>
	{/if}
</div>
