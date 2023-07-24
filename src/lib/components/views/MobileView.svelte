<script lang="ts">
	import { marked } from 'marked';
	import { rawMarkdown } from '$lib/stores/store';

	import editIconUrl from '$lib/assets/editIcon.svg?url';
	import previewIconUrl from '$lib/assets/previewIcon.svg?url';

	let mobileToggleView = false;
</script>

<div class="h-full w-full flex flex-col">
	<div class=" w-full h-14 flex">
		<input class="w-full px-3 text-xl" type="text" value="Filename" />
	</div>

	<div class="h-full w-full inline overflow-x-hidden whitespace-nowrap">
		<div
			class={`h-full w-full inline-block transition-transform ${
				mobileToggleView && '-translate-x-full'
			}`}
		>
			<textarea
				bind:value={$rawMarkdown}
				placeholder="Start typing now..."
				class="h-full bg-zinc-200 w-full text-md p-3 font-mono resize-none focus:outline-none appearance-none"
			/>
		</div>
		<!-- DO NOT REMOVE THESE COMMENT LINES BECAUSE SPACE MATTERS!!!
		-->
		<article
			class={`h-full bg-white inline-block transition-transform align-top prose font-serif prose-xl prose-headings w-full whitespace-normal p-5 ${
				mobileToggleView && '-translate-x-full'
			} `}
		>
			{@html marked.parse($rawMarkdown, { mangle: false, headerIds: false })}
		</article>
	</div>

	<div class="w-full flex justify-center items-center h-20 md:hidden">
		<div class="flex align-middle items-center">
			<img alt="Edit" src={editIconUrl} class="mr-6 w-6" />
			<label class="relative inline-flex items-center cursor-pointer">
				<input type="checkbox" bind:checked={mobileToggleView} class="sr-only peer" />
				<div
					class="w-14 h-7 peer-focus:ring-4 rounded-full peer bg-zinc-700 peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-0.5 after:left-[4px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-6 after:w-6 after:transition-all border-zinc-600"
				/>
			</label>
			<img alt="Preview" src={previewIconUrl} class="ml-6 w-6" />
		</div>
	</div>
</div>
