<!-- This is the global layout file; it "wraps" every page on the site. (Or more accurately: is the parent component to every page component on the site.) -->
<script context="module">
	export const load = async ({ url, fetch }) => {
		/**
		 * This fetch call is not used in this file, but the route won't be pre-rendered
		 * and routed properly unless it's called inside a `load` function. ¯\_(ツ)_/¯
		 * */
		const rss = await fetch(`/api/rss.xml`);

		return {
			props: {
				path: url.pathname
			}
		};
	};
</script>

<script>
	import '$lib/assets/scss/global.scss';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import { currentPage, isMenuOpen } from '$lib/assets/js/store';
	import { navItems } from '$lib/config';
	import { prefetch } from '$app/navigation';
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	const transitionIn = { delay: 150, duration: 150 };
	const transitionOut = { duration: 100 };

	export let path;

	/**
	 * Updates the global store with the current path. (Used for highlighting
	 * the current page in the nav, but could be useful for other purposes.)
	 **/
	$: currentPage.set(path);

	// For gtag updates when the client changes pages
	$: {
		if (typeof gtag !== 'undefined') {
			gtag('config', 'G-M6S4SP5GVN', {
				page_path: $currentPage.path
			});
		}
	}
	/**
	 * This pre-fetches all top-level routes on the site in the background for faster loading.
	 * https://kit.svelte.dev/docs#modules-$app-navigation
	 *
	 * Any route added in src/lib/config.js will be prefetched automatically. You can add your
	 * own prefetch() calls here, too.
	 **/
	onMount(() => {
		navItems.forEach((item) => prefetch(item.route));

		// <!--Start of Tawk.to Script-->
		var Tawk_API = Tawk_API || {},
			Tawk_LoadStart = new Date();
		(function () {
			var s1 = document.createElement('script'),
				s0 = document.getElementsByTagName('script')[0];
			s1.async = true;
			s1.src = 'https://embed.tawk.to/62c2cca6b0d10b6f3e7ab043/1g74eur6h';
			s1.charset = 'UTF-8';
			s1.setAttribute('crossorigin', '*');
			s0.parentNode.insertBefore(s1, s0);
		})();
		// <!--End of Tawk.to Script-->
	});
</script>

<!-- 
  The below markup is used on every page in the site. The <slot> is where the page's
  actual contents will show up.
-->
<div class="layout" class:open={$isMenuOpen}>
	<Header />
	{#key path}
		<main id="main" tabindex="-1" in:fade={transitionIn} out:fade={transitionOut}>
			<slot />
		</main>
	{/key}
	<Footer />
</div>
