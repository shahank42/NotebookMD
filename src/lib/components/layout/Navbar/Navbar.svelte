<script lang="ts">
	import DesktopNavbar from './DesktopNavbar.svelte';
	import MobileNavbar from './MobileNavbar.svelte';
</script>

<main class="md:hidden">
	<MobileNavbar />
</main>

<main class="hidden md:flex">
	<DesktopNavbar />
</main>
