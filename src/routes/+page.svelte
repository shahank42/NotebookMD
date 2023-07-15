<script lang="ts">
	import { marked } from 'marked';

	let rawMarkdown = '';

	let titleBarHeight = 0;
</script>

<main class="min-h-screen flex w-full">
	<div class="bg-zinc-500 w-64">Files</div>
	<div class="flex flex-col h-auto w-full">
		<div class="bg-zinc-400" bind:clientHeight={titleBarHeight}>
			<p class="text-3xl p-3">Title</p>
		</div>
		<div class="flex h-full w-full">
			<textarea
				bind:value={rawMarkdown}
				placeholder="Start typing now..."
				class="bg-zinc-100 text-md w-0 flex-grow p-3 font-mono resize-none focus:outline-none appearance-none"
			/>
			<article class={`w-0 flex-grow prose p-5 font-serif prose-xl prose-headings max-w-none max-h-[calc(100dvh-${titleBarHeight}px)] overflow-y-scroll`}>
				{@html marked.parse(rawMarkdown, { mangle: false, headerIds: false })}
			</article>
		</div>
	</div>
</main>
