<script lang="ts">
	import { fade, scale } from 'svelte/transition';
	import { onMount, onDestroy } from 'svelte';
	import { cn } from '$lib/utils';

	let { className = '', open = false, children } = $props();

	function onClose() {
		const event = new CustomEvent('modalClose');
		window.dispatchEvent(event);
	}

	function handleKeydown(e: KeyboardEvent) {
		if (e.key === 'Escape' && open) {
			onClose();
		}
	}

	function handleOutsideClick(e: MouseEvent) {
		const target = e.target as HTMLElement;
		if (target.classList.contains('modal-backdrop')) {
			onClose();
		}
	}

	onMount(() => {
		document.addEventListener('keydown', handleKeydown);
	});

	onDestroy(() => {
		document.removeEventListener('keydown', handleKeydown);
	});
</script>

{#if open}
	<div
		class="fixed inset-0 z-50 flex items-center justify-center modal-backdrop bg-black/80 backdrop-blur-sm"
		role="dialog"
		aria-modal="true"
		aria-labelledby="modal-title"
		onclick={handleOutsideClick}
		onkeydown={handleKeydown}
		in:fade={{ duration: 200 }}
		out:fade={{ duration: 200 }}
	>
		<div
			class={cn('relative bg-transparent overflow-hidden max-w-[90vw] max-h-[90vh]', className)}
			in:scale={{ start: 0.95, duration: 200 }}
			out:scale={{ start: 1, end: 0.95, duration: 200 }}
		>
			{@render children()}

			<button
				type="button"
				class="absolute top-4 right-4 bg-black/50 backdrop-blur-sm text-white w-10 h-10 rounded-full flex items-center justify-center border border-white/10 hover:border-white/30 transition-all"
				onclick={onClose}
				aria-label="Close modal"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="24"
					height="24"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
					class="w-5 h-5"
					><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"
					></line></svg
				>
			</button>
		</div>
	</div>
{/if}
