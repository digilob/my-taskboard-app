<script>
	import { flip } from 'svelte/animate';
	import { dndzone } from 'svelte-dnd-action';
	import Column from './Column.svelte';



	export let columns;
	// will be called any time a card or a column gets dropped to update the parent data
	export let onFinalUpdate;

	function handleDndConsiderColumns(e) {
		columns = e.detail.items;
	}
	function handleDndFinalizeColumns(e) {
		onFinalUpdate(e.detail.items);
	}
	function handleItemFinalize(columnIdx, newItems) {
		columns[columnIdx].items = newItems;
		onFinalUpdate([...columns]);
	}

	const flipDurationMs = 300;

	function handleDndConsider(e) {
		tasks = e.detail.items;
	}

	function handleDndFinalize(e) {
		tasks = e.detail.items;
	}
</script>

	<div class="task-board" 
		use:dndzone={{items:columns, flipDurationMs, type:'column'}} 
		on:consider={handleDndConsiderColumns} 
		on:finalize={handleDndFinalizeColumns}>
		    {#each columns as {id, name,items}, idx (id)}
				<div class="task-list"
					animate:flip="{{duration: flipDurationMs}}" >    
								<Column name={name} items={items} onDrop={(newItems) => handleItemFinalize(idx, newItems)} />
					</div>
				{/each}
	</div>

<style>
	.task-board {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
		gap: 1rem;
		padding: 1rem;
	}
	.task-list {
		display: flex;
		flex-direction: column;
		align-items: center;
		border-radius: 5px;
		overflow: scroll;
		height: 400px;
	}

	.task-list h2 {
		color: #fff;
		font-size: 1.5rem;
		margin: 0;
		padding: 0.5rem;
		text-align: center;
		text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.4);
	}

</style>
