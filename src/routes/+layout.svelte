<script>
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte';
</script>

<Navbar />

<div class="my-4 pt-5">
	<slot />
</div>

<Footer />
