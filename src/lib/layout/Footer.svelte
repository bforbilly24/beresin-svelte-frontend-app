<script>
	import GitHubSvg from '$lib/imgs/github-dark.svg';
	import BeresInBrand from '$lib/imgs/BeresInBrand.svg';
	import TwitterSvg from '$lib/imgs/x.svg';

	const footerNavs = [
		{
			label: 'Service',
			items: [
				{
					href: '#boost-listing',
					name: 'Boost Listing'
				},
				{
					href: '/faq',
					name: 'FAQ'
				}
			]
		},

		{
			label: 'Connect With Us',
			items: [
				{
					href: 'https://github.com/beresindev',
					name: 'Github'
				},
				{
					href: 'https://wa.me/6287709999050',
					name: 'Whatsapp'
				},
				{
					href: 'mailto:teamberesin@gmail.com',
					name: 'Email'
				}
			]
		},
		{
			label: 'Legal',
			items: [
				{
					href: '/terms',
					name: 'Terms'
				},

				{
					href: '/privacy',
					name: 'Privacy'
				}
			]
		}
	];

	const footerSocials = [
		{
			href: 'https://github.com/beresindev',
			name: 'Github',
			icon: GitHubSvg
		},
	];
</script>

<footer>
	<div class="mx-auto w-full max-w-screen-xl xl:pb-2">
		<div class="gap-4 p-4 px-8 py-16 sm:pb-16 md:flex md:justify-between">
			<div class="mb-12 flex flex-col gap-4">
				<a href="https://animation-svelte.vercel.app" class="flex items-center gap-2">
					<img
						alt="BeresIn"
						src={BeresInBrand}
						class="h-14 w-14 px-2 dark:brightness-0 dark:invert"
						width={28}
						height={8}
					/>
					<span class="self-center whitespace-nowrap text-2xl font-semibold dark:text-white">
						Beresin
					</span>
				</a>
				<p class="max-w-xs">Solusi Jasa Kampus, Dari Mahasiswa untuk Mahasiswa!</p>
			</div>
			<div class="grid grid-cols-1 gap-8 sm:grid-cols-3 sm:gap-10">
				{#each footerNavs as nav}
					<div>
						<h2
							class="mb-6 text-sm font-medium uppercase tracking-tighter text-gray-900 dark:text-white"
						>
							{nav.label}
						</h2>
						<ul class="grid gap-2">
							{#each nav.items as item}
								<li>
									<a
										href={item.href}
										class="cursor-pointer text-sm font-[450] text-gray-400 duration-200 hover:text-gray-200"
									>
										{item.name}
									</a>
								</li>
							{/each}
						</ul>
					</div>
				{/each}
			</div>
		</div>

		<div
			class="flex flex-col gap-2 rounded-md border-neutral-700/20 px-8 py-4 sm:flex sm:flex-row sm:items-center sm:justify-between"
		>
			<div class="flex items-center space-x-5 sm:mt-0 sm:justify-center">
				{#each footerSocials as social}
					<a
						href={social.href}
						class="fill-gray-500 text-gray-500 hover:fill-gray-900 hover:text-gray-900 dark:hover:fill-gray-600 dark:hover:text-gray-600"
					>
						<img src={social.icon} class="size-4" alt={social.name} />
						<span class="sr-only">{social.name}</span>
					</a>
				{/each}
			</div>
			<span class="text-sm text-gray-500 dark:text-gray-400 sm:text-center">
				Copyright ©
				{' '}
				{new Date().getFullYear()}
				{' '}
				<a href="/" class="cursor-pointer">BeresIn</a>
				. All Rights Reserved.
			</span>
		</div>
	</div>
	<!-- Site Banner -->
</footer>
