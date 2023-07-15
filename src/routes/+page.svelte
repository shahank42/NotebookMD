<script lang="ts">
	import { marked } from 'marked';

	let rawMarkdown = "";
</script>

<main class="h-64 flex flex-grow w-full bg-zinc-800">
	<div class="bg-zinc-600 w-0 flex-grow">
		<textarea class="w-full h-full" bind:value={rawMarkdown} />
	</div>
	<div class="bg-zinc-400 w-0 flex-grow">
		{@html marked.parse(rawMarkdown, { mangle: false, headerIds: false })}
	</div>
</main>
