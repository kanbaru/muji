<script lang="ts">
	import CodeMirror from 'svelte-codemirror-editor';
	import { markdown } from '@codemirror/lang-markdown';
	let wrap = true;
	let value = '';
	import { EditorView, keymap, placeholder as placeholderExt } from '@codemirror/view';
	import { indentWithTab, history, historyKeymap, defaultKeymap } from '@codemirror/commands';
	import { syntaxHighlighting, defaultHighlightStyle } from '@codemirror/language';
	import { search, searchKeymap } from '@codemirror/search';
</script>

<div class="root">
	<div class="box">
		<CodeMirror
			bind:value
			lang={markdown()}
			basic={false}
			extensions={[
				keymap.of([indentWithTab, ...historyKeymap, ...defaultKeymap, ...searchKeymap]),
				search(),
				syntaxHighlighting(defaultHighlightStyle, { fallback: true }),
				history()
			]}
			styles={{
				'.cm-gutters': {
					backgroundColor: 'white',
					hidden: 'true'
				},
				'.cm-line': {
					maxHeight: 'max-content',
					whiteSpace: 'break-spaces',
					maxWidth: '90vw',
					overflowWrap: 'break-word',
					hyphens: 'auto'
				}
			}}
		/>
	</div>
</div>

<style>
	.root {
		color: #001030;
		height: 96vh;
	}
    .box {
        display: table-cell;
        vertical-align: middle;
        color: #001030;
		height: 96vh;
    }
</style>
