<!-- https://tute.io/google-analytics-svelte-sapper -->
<script>
  import { stores } from '@sapper/app';
  const { page } = stores();
  $: {
    if (typeof gtag !== "undefined"){
      gtag("config", "G-M6S4SP5GVN", {
        page_path: $page.path
      });
    }
  }
</script>