<script lang="ts">
	import { ArrowRightIcon, Download } from 'lucide-svelte';
	import AnimatedShinyText from '$lib/components/magic/AnimatedShinyText/AnimatedShinyText.svelte';
	import BorderBeam from '$lib/components/magic/borderbeam/BorderBeam.svelte';
	import Button from '$lib/components/ui/button/button.svelte';
	import Spotlight from '../magic/Spotlight/Spotlight.svelte';
	import HeroVideoDialog from '../magic/HeroVideoDialog/HeroVideoDialog.svelte';
	import type { ObserverEventDetails } from 'svelte-inview';
	import { inview } from 'svelte-inview';

	// Images
	let inView = false;
	const handleChange = ({ detail }: CustomEvent<ObserverEventDetails>) => {
		// console.log(detail);
		inView = detail.inView;
	};
</script>

<section id="hero" class="relative mx-auto mt-32 max-w-7xl px-6 text-center md:px-8">
	<Spotlight />
	<div
		class="backdrop-filter-[12px] group inline-flex h-7 -translate-y-4 animate-fade-in items-center justify-between gap-1 rounded-full border border-white/5 bg-white/10 px-3 text-xs text-white opacity-0 transition-all ease-in hover:cursor-pointer hover:bg-white/20 dark:text-black"
	>
		<AnimatedShinyText class="inline-flex items-center justify-center">
			<span>✨ Memperkenalkan BeresIn App</span>
			<ArrowRightIcon
				class="ml-1 size-3 transition-transform duration-300 ease-in-out group-hover:translate-x-0.5"
			/>
		</AnimatedShinyText>
	</div>
	<h1
		id="downloadapp"
		class="-translate-y-4 animate-fade-in text-balance bg-gradient-to-br from-black from-30% to-black/40 bg-clip-text py-6 text-5xl font-medium leading-none tracking-tighter text-transparent opacity-0 [--animation-delay:200ms] dark:from-white dark:to-white/40 sm:text-6xl md:text-7xl lg:text-8xl"
	>
		Solusi Jasa Kampus
		<br class="hidden md:block" />
		Dari Mahasiswa untuk Mahasiswa!
	</h1>
	<p
		class="mb-12 -translate-y-4 animate-fade-in text-balance text-lg tracking-tight text-gray-400 opacity-0 [--animation-delay:400ms] md:text-xl"
	>
		Aplikasi marketplace berbasis mobile yang memudahkan mahasiswa menemukan dan menawarkan berbagai
		<br class="hidden md:block" />
		jasa di kampus dengan
		<span class="underline underline-offset-2">mudah,</span>
		<span class="underline underline-offset-2"> cepat,</span> dan
		<span class="underline underline-offset-2">terpercaya</span>. Temukan solusi terbaik dari sesama
		mahasiswa untuk kebutuhan akademik maupun non-akademik dalam satu platform!
	</p>
	<Button
		class="-translate-y-4 animate-fade-in gap-x-2 rounded-lg text-white opacity-0 ease-in-out [--animation-delay:600ms] dark:text-black"
	>
		<Download class='w-4 h-4' />
		<span>Unduh</span>
		<ArrowRightIcon
			class="ml-1 size-4 transition-transform duration-300 ease-in-out group-hover:translate-x-1"
		/>
	</Button>
	<div
		use:inview={{
			unobserveOnEnter: true,
			rootMargin: '-100px'
		}}
		on:inview_change={handleChange}
		class="relative mt-32 animate-fade-up opacity-0 [--animation-delay:400ms] [perspective:2000px]"
	>
		<div
			class="rounded-xl border-2 border-gray-600/20 dark:border-gray-100/20 bg-white bg-opacity-[0.01] before:absolute before:bottom-0 before:left-0 before:top-0 before:size-full before:h-[80%] before:w-full before:opacity-0 before:[background-image:linear-gradient(to_bottom,var(--color-one),var(--color-one),transparent_40%)] before:[filter:blur(180px)] after:absolute after:bottom-0 after:left-0 after:z-0 after:h-[45%] after:w-full after:[background:linear-gradient(to_top,hsl(var(--background))_20%,transparent)] {inView
				? 'before:animate-image-glow'
				: ''}"
		>
			<BorderBeam
				size={200}
				duration={12}
				delay={0}
				colorFrom="var(--color-one)"
				colorTo="var(--color-two)"
			/>

			<HeroVideoDialog
				animationStyle="from-center"
				videoSrc="https://www.youtube.com/embed/qh3NGpYRG3I?si=4rb-zSdDkVK9qxxb"
				thumbnailSrc="src/lib/imgs/banner.png"
				thumbnailAlt="Hero Video"
			/>
		</div>
	</div>
</section>
