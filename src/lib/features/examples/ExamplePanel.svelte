<script lang="ts">
	import Modal from '$lib/components/utilities/Modal.svelte';
	import { shortcut } from '$lib/helpers/shortcut';
	import { reset } from '../editor/editor.store';
	import { examples } from './constants';
	import { exampleModal, toggleExamplePanel } from './modal.store';

	function replace(str) {
		reset(str);
		toggleExamplePanel();
	}
</script>

<button
	class="radius-1 bg-grey-4 pointer lh-0 hover:text-primary transition-300"
	on:click={toggleExamplePanel}
	use:shortcut={{ key: 'e', callback: toggleExamplePanel }}
	data-tooltip="ctrl + E"
>
	examples
</button>
<Modal store={exampleModal}>
	<div class="flex-col p-0">
		<span class="text-0 bold">State machine examples</span>
		<ul class="list">
			{#each examples as example}
				<li class="flex-row items-center py-000 border-b-grey-4 gap-000">
					<button
						on:click={() => replace(example.config)}
						class="pointer transition-300 text-00 radius-000 bg-grey-3 hover:bg-primary hover:text-grey-5 text-grey-0 hover:text-grey-0"
					>
						{example.title}
					</button>
					<span class="text-grey-3 text-00">{example.description}</span>
				</li>
			{/each}
		</ul>
	</div>
</Modal>
