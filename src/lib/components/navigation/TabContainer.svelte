<script lang="ts">
	import type { SvelteComponent } from 'svelte';

	type Item = {
		label: string;
		component: typeof SvelteComponent;
	};

	let className: string = '';
	export { className as class };
	export let items: Item[] = [];
	let selected: string = items[0].label;
</script>

<div class="flex-row gap-00 items-center mb-0 {className}">
	<slot />
	<ul class="container | flex-row border-w-3 border-grey-5 bg-grey-5 radius-00">
		{#each items as item}
			<li>
				<button
					class:selected={selected === item.label}
					class="item"
					on:click={() => (selected = item.label)}
				>
					{item.label}
				</button>
			</li>
		{/each}
	</ul>
</div>

<div class="flex-grow flex-col bg-grey-5 radius-0">
	{#each items as item}
		{#if item.label === selected}
			<svelte:component this={item.component} />
		{/if}
	{/each}
</div>

<style>
	.container {
		gap: 3px;
	}

	.item {
		padding: var(--size-none) var(--size-1);
		cursor: pointer;
		background: transparent;
		border-radius: var(--size-000);
		color: var(--color-grey-0);
		transition: var(--transition-300);
	}

	.selected {
		background-color: var(--color-primary);
		color: var(--color-grey-0);
	}

	.item:hover,
	.selected:hover {
		background: var(--color-grey-4);
		color: var(--color-primary);
	}
</style>
