<script lang="ts">
	import { onMount } from 'svelte';
	import BeresIn from '$lib/imgs/BeresIn.svg';
	import { writable } from 'svelte/store';
	import Sun from 'lucide-svelte/icons/sun';
	import Moon from 'lucide-svelte/icons/moon';
	import { Button } from '$lib/components/ui/button/index';

	const darkMode = writable(false);

	onMount(() => {
		const storedTheme = localStorage.getItem('theme');
		if (storedTheme === 'dark') {
			darkMode.set(true);
			document.documentElement.classList.add('dark');
		} else {
			darkMode.set(false);
			document.documentElement.classList.remove('dark');
		}
	});

	// Toggle dark mode
	function toggleDarkMode() {
		darkMode.update((current) => {
			const newMode = !current;
			if (newMode) {
				localStorage.setItem('theme', 'dark');
				document.documentElement.classList.add('dark');
			} else {
				localStorage.setItem('theme', 'light');
				document.documentElement.classList.remove('dark');
			}
			return newMode;
		});
	}

	const menuItem = [
		{
			id: 1,
			label: 'Features',
			href: '#'
		}
	];

	let innerWidth = 0;
</script>

<svelte:window bind:innerWidth />

<header
	class="fixed left-0 top-0 z-50 w-full -translate-y-4 animate-fade-in border-b opacity-0 backdrop-blur-md"
>
	<div
		class="container flex h-10 items-center lg:h-20 {innerWidth < 768
			? 'justify-center'
			: 'justify-between'}"
	>
		<a href="/">
			<div class="text-md flex flex-row items-center gap-x-2 font-semibold">
				<img
					alt="BeresIn"
					src={BeresIn}
					class="h-8 w-24 px-2 dark:brightness-0 dark:invert lg:h-14 lg:w-32"
					width={28}
					height={8}
				/>
			</div>
		</a>

		{#if innerWidth >= 768}
			<Button on:click={toggleDarkMode} variant="theme" size="icon" class="relative">
				<Sun
					class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
				/>
				<Moon
					class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
				/>
			</Button>
		{/if}
	</div>
</header>

{#if innerWidth < 768}
	<Button
		on:click={toggleDarkMode}
		variant="theme"
		size="icon"
		class="fixed bottom-4 right-4 z-50 rounded-full bg-gray-800 p-3 text-white shadow-lg hover:bg-gray-700"
	>
		<Sun
			class="h-[1.5rem] w-[1.5rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
		/>
		<Moon
			class="absolute h-[1.5rem] w-[1.5rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
		/>
	</Button>
{/if}
