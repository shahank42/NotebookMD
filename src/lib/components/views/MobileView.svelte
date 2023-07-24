<script lang="ts">
	import { marked } from 'marked';
	import { rawMarkdown } from '$lib/stores/store';

	import editIconUrl from '$lib/assets/editIcon.svg?url';
	import previewIconUrl from '$lib/assets/previewIcon.svg?url';
	import fileIconUrl from '$lib/assets/fileIcon.svg?url';
	import { afterUpdate } from 'svelte';

	import CodeMirror from 'svelte-codemirror-editor';

	import { markdown } from '@codemirror/lang-markdown';
	import { languages } from '@codemirror/language-data';

	let mdEditorViewNode: HTMLElement;
	let toggleEdit = false;

	afterUpdate(() => {
		mdEditorViewNode.scrollTo({ top: 0 });
	});
</script>

<div class="h-full w-full flex flex-col">
	<div class=" w-full h-14 flex">
		<!-- <button class="bg-zinc-100 hover:focus:bg-zinc-300 w-14 flex justify-center align-middle">
			<img alt="Files" src={fileIconUrl} class="w-5" />
		</button> -->
		<input
			class="w-full px-4 text-xl focus:outline-none appearance-none bg-zinc-100"
			type="text"
			value=""
			placeholder="Untitled Note"
		/>
	</div>

	<div
		bind:this={mdEditorViewNode}
		class={`h-[calc(100dvh)] w-full inline overflow-x-hidden whitespace-nowrap ${
			toggleEdit && 'overflow-y-hidden'
		}`}
	>
		<article
			class={`h-full bg-white inline-block transition-transform align-top prose prose-base prose-headings w-full whitespace-normal p-5 ${
				toggleEdit && '-translate-x-full'
			} `}
		>
			{@html marked.parse($rawMarkdown, { mangle: false, headerIds: false })}
		</article><!-- DO NOT REMOVE THESE COMMENT LINES BECAUSE SPACE MATTERS!!!
		--><div
			class={`h-full w-full inline-block transition-transform ${toggleEdit && '-translate-x-full'}`}
		>
			<CodeMirror
				bind:value={$rawMarkdown}
				class="h-full text-base overflow-y-scroll"
				lang={markdown()}
				lineWrapping={true}
				styles={{
					'&': {
						height: '100%'
					}
				}}
			/>
		</div>
		
	</div>

	<div class="w-full bg-zinc-300 flex justify-center items-center h-20 md:hidden">
		<div class="flex align-middle items-center">
			<img alt="Edit" src={previewIconUrl} class="mr-6 w-6" />
			<label class="relative inline-flex items-center cursor-pointer">
				<input type="checkbox" bind:checked={toggleEdit} class="sr-only peer" />
				<div
					class="w-14 h-7 peer-focus:ring-4 rounded-full peer bg-zinc-700 peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-0.5 after:left-[4px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-6 after:w-6 after:transition-all border-zinc-600"
				/>
			</label>
			<img alt="Preview" src={editIconUrl} class="ml-6 w-6" />
		</div>
	</div>
</div>
