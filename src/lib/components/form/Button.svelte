<script lang="ts">
	let className: string = '';
	export { className as class };
	export let type: string = '';
	export let role: string = 'button';
</script>

<button
	class="radius-1 px-1 transition-300 pointer {className} border-primary border-w-00"
	{role}
	data-type={type}
	on:click
>
	<slot />
</button>

<style>
	button {
		--bg: var(--color-primary);
		--fg: var(--color-secondary);

		background-color: var(--bg);
		color: var(--fg);
		cursor: pointer;
	}

	button:hover {
		background-color: var(--fg);
		color: var(--bg);
	}

	button[data-type~='secondary'] {
		--bg: var(--color-secondary);
		--fg: var(--color-primary);
	}
</style>
