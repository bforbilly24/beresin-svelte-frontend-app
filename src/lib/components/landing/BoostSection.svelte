<script lang="ts">
	import { LoaderIcon, CheckIcon } from 'lucide-svelte';
	import Switch from '$lib/components/ui/switch/switch.svelte';
	import Button from '$lib/components/ui/button/button.svelte';
	import { cn } from '$lib/utils';
	import { fly } from 'svelte/transition';
	import MagicCard from '../magic/MagicCard/MagicCard.svelte';

	export function toHumanPrice(price: number) {
		return new Intl.NumberFormat('id-ID', {
			style: 'currency',
			currency: 'IDR',
			minimumFractionDigits: 0,
			maximumFractionDigits: 0
		}).format(price);
	}

	const WHATSAPP_NUMBER = '+6287709999050';

	let productBoosts = [
		{
			id: 1,
			boost_name: 'Boost Dasar',
			duration: 1,
			price: 6999,
			description: 'Boost cepat untuk visibilitas instan',
			features: [
				'1 hari boost',
				'Peningkatan profil dasar',
				'Jangkauan terbatas',
				'Targeting standar'
			],
			isMostPopular: false
		},
		{
			id: 3,
			boost_name: 'Boost Premium',
			duration: 7,
			price: 9999,
			description: 'Boost terbaik untuk eksposur maksimal',
			features: [
				'7 hari boost',
				'Penyorotan profil premium',
				'Targeting canggih',
				'Jangkauan pengguna yang luas',
				'Support prioritas'
			],
			isMostPopular: true
		},
		{
			id: 2,
			boost_name: 'Boost Standar',
			duration: 5,
			price: 8999,
			description: 'Boost komprehensif untuk jangkauan lebih luas',
			features: [
				'5 hari boost',
				'Peningkatan visibilitas profil',
				'Targeting yang lebih luas',
				'Peningkatan keterlibatan pengguna'
			],
			isMostPopular: false
		}
	];

	let isLoading = false;
	let index: string = '';

	let onSubscribeClick = async (boost: (typeof productBoosts)[0]) => {
		index = boost.id.toString();
		isLoading = true;

		// Construct WhatsApp message
		const message = `Saya ingin plan: ${boost.boost_name}, Username: ('Username Anda'), Nama Jasa: ('Service Anda')`;

		// Encode the message for URL
		const encodedMessage = encodeURIComponent(message);

		// Open WhatsApp with the pre-filled message
		const whatsappUrl = `https://wa.me/${WHATSAPP_NUMBER}?text=${encodedMessage}`;

		// Simulate loading and then redirect
		await new Promise((resolve) => setTimeout(resolve, 1000));

		// Open WhatsApp in a new tab
		window.open(whatsappUrl, '_blank');

		isLoading = false;
	};
</script>

<section id="boost-listing">
	<div class="mx-auto flex max-w-screen-xl flex-col gap-8 px-4 py-14 md:px-8">
		<div class="mx-auto max-w-5xl text-center">
			<h4 class="text-xl font-bold tracking-tight text-black dark:text-white">Harga Boost</h4>

			<h2 class="text-5xl font-bold tracking-tight text-black dark:text-white sm:text-6xl">
				Sorot Jasa Anda ke Puncak Atas
			</h2>

			<p class="mt-6 text-xl leading-8 text-black/80 dark:text-white">
				Pilih <strong>paket boost</strong> untuk meningkatkan layanan Anda, sorot di bagian atas, dan
				pastikan lebih banyak pengguna yang memperhatikannya untuk visibilitas maksimal.
			</p>
		</div>

		<div class="mx-auto grid w-full flex-col justify-center gap-4 sm:grid-cols-2 lg:grid-cols-3">
			{#each productBoosts as boost, index}
				<MagicCard
					class={cn(
						'group cursor-pointer flex-col items-center justify-center whitespace-nowrap border text-4xl shadow-2xl transition-all duration-300 hover:border-gray-200',
						{
							'border-2 border-gray-600 transition-all duration-500 dark:border-gray-200':
								boost.isMostPopular
						}
					)}
					gradientColor="#043634"
					gradientSize={300}
				>
					<div
						class="relative flex max-w-[400px] flex-col gap-8 overflow-hidden rounded-2xl p-4 text-black dark:text-white"
					>
						<div class="flex items-center">
							<div class="ml-4">
								<h2 class="text-base font-semibold leading-7">
									{boost.boost_name}
								</h2>
								<p class="h-12 text-sm leading-5 text-black/70 dark:text-white">
									{boost.description}
								</p>
							</div>
						</div>
						{#key boost.id}
							<div in:fly={{ y: 20, duration: 300, delay: index * 40 }} class="flex flex-row gap-1">
								<span class="text-4xl font-bold text-black dark:text-white">
									{toHumanPrice(boost.price)}
									<span class="text-xs">
										/ {boost.duration} hari{boost.duration > 1 ? '' : ''}
									</span>
								</span>
							</div>
						{/key}

						<Button
							class={cn(
								'group relative w-full gap-2 overflow-hidden text-lg font-semibold tracking-tighter',
								'transform-gpu ring-offset-current transition-all duration-300 ease-out hover:ring-2 hover:ring-primary hover:ring-offset-2'
							)}
							disabled={isLoading}
							on:click={() => onSubscribeClick(boost)}
						>
							<span
								class="absolute right-0 -mt-12 h-32 w-8 translate-x-12 rotate-12 transform-gpu bg-white opacity-10 transition-all duration-1000 ease-out group-hover:-translate-x-96 dark:bg-black"
							/>
							{#if isLoading && index === boost.id}
								<LoaderIcon class="mr-2 size-4 animate-spin" />
								Mendaftar
							{:else}
								Boost Sekarang
							{/if}
						</Button>

						<hr
							class="m-0 h-px w-full border-none bg-gradient-to-r from-neutral-200/0 via-neutral-500/30 to-neutral-200/0"
						/>
						{#if boost.features && boost.features.length > 0}
							<ul class="flex flex-col gap-2 font-normal">
								{#each boost.features as feature}
									<li
										class="flex items-center gap-3 text-xs font-medium text-black dark:text-white"
									>
										<CheckIcon
											class="size-5 shrink-0 rounded-full bg-green-400 p-[2-px] text-black dark:text-white"
										/>
										<span class="flex">{feature}</span>
									</li>
								{/each}
							</ul>
						{/if}
					</div>
				</MagicCard>
			{/each}
		</div>
	</div>
</section>
