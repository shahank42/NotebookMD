<script lang="ts">
	import MobileView from '$lib/components/views/MobileView.svelte';
	import DesktopView from '$lib/components/views/DesktopView.svelte';
</script>

<main class="md:hidden h-[100dvh]">
	<MobileView />
</main>

<main class="hidden md:flex h-[100dvh]">
	<DesktopView />
</main>