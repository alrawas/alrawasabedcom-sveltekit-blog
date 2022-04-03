<script context="module">
  export const load = async () => {
		const HomeFile = await import('../../HOME.md');
    const Home = HomeFile.default;

		return {
			props: {
				Home
			}
		}
	}
</script>

<script>
  export let Home
</script>


<svelte:head>
	<title>SvelteKit Static Blog Starter</title>
</svelte:head>


<svelte:component this={Home} />
<!-- This is the README.md file in the root of the repo. It serves double duty as the homepage's content. If you'd rather use your own HTML and/or Svelte, you can delete/modify everything above this line. -->