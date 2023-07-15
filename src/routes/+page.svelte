<script lang="ts">
	import { marked } from 'marked';

	let rawMarkdown = "";
</script>

<main class="h-[99dvh] flex w-full">
	<div class="w-0 flex-grow">
		<textarea class="bg-zinc-100 w-full h-full p-3 font-mono resize-none focus:outline-none appearance-none" bind:value={rawMarkdown} />
	</div>
	<div class="w-0 flex-grow prose max-w-none p-3 overflow-y-scroll">
		{@html marked.parse(rawMarkdown, { mangle: false, headerIds: false })}
	</div>
</main>
