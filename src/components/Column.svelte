<script>
	import { flip } from 'svelte/animate';
	import { dndzone } from 'svelte-dnd-action';
	const flipDurationMs = 150;
	export let name;
	export let items;
	export let onDrop;

	function handleDndConsiderCards(e) {
		console.warn('got consider', name);
		items = e.detail.items;
	}
	function handleDndFinalizeCards(e) {
		onDrop(e.detail.items);
	}
</script>

<div class="wrapper">
	<div class="column-title">
		{name}
	</div>
	<div
		class="column-content task-list"
		class:todo={name === 'TODO'}
		class:in-dev={name === 'INDEV'}
		class:done={name === 'DONE'}
		use:dndzone={{ items, flipDurationMs, zoneTabIndex: -1 }}
		on:consider={handleDndConsiderCards}
		on:finalize={handleDndFinalizeCards}
	>
		{#each items as item (item.id)}
			<div class="task" animate:flip={{ duration: flipDurationMs }}>
				{item.name}
			</div>
		{/each}
	</div>
</div>

<style>
	.wrapper {
		height: 100%;
		width: 100%;
		/* Notice we make sure this container doesn't scroll so that the title stays on top and the dndzone inside is scrollable */
		overflow-y: hidden;
	}

	.column-content {
		height: calc(100% - 2.5em);
		/* Notice that the scroll container needs to be the dndzone if you want dragging near the edge to trigger scrolling */
		overflow-y: scroll;
	}

	.column-title {
		height: 2.5em;
		font-weight: bold;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: #4831d4;
		color: white;
	}

	.task-list .task {
		background-color: #f0f0f0;
		border: 1px solid #ccc;
		border-radius: 5px;
		padding: 1rem;
		margin: 1rem 0;
		cursor: grab;
		width: 100%;
	}

	.task-list .task:hover {
		background-color: #eee;
	}

	.task-list .task:active {
		cursor: grabbing;
	}

	.task-list .task h3 {
		font-size: 1.2rem;
		margin: 0;
		padding: 0;
	}

	.task-list .task p {
		font-size: 0.9rem;
		margin: 0.5rem 0 0 0;
		padding: 0;
	}

	.task-list .task.done {
		text-decoration: line-through;
	}

	.task-list.todo {
		background: linear-gradient(to bottom right, #ccf381, #72bf44);
	}

	.task-list.in-dev {
		background: linear-gradient(to bottom right, #6dd5f7, #9ccfff);
	}

	.task-list.done {
		background: linear-gradient(to bottom right, #f7d66d, #ffc99c);
	}
</style>
