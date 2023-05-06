<script>
	import TaskBoard from '../components/TaskBoard.svelte';
	let columnsData = [
		{
			id: 'c1',
			name: 'TODO',
			items: [
				{ id: 1, name: 'item41' },
				{ id: 2, name: 'item42' },
				{ id: 3, name: 'item43' },
				{ id: 4, name: 'item44' },
				{ id: 5, name: 'item45' },
				{ id: 6, name: 'item46' },
				{ id: 7, name: 'item47' },
				{ id: 8, name: 'item48' },
				{ id: 9, name: 'item49' }
			]
		},
		{
			id: 'c2',
			name: 'INDEV',
			items: [
				{ id: 10, name: 'item50' },
				{ id: 11, name: 'item51' }
			]
		},
		{
			id: 'c3',
			name: 'DONE',
			items: [{ id: 13, name: 'item52' }]
		}
	];

	function handleBoardUpdated(newColumnsData) {
		// if you wanted to update a database or a server, this is where you would do it
		columnsData = newColumnsData;
	}
</script>

<div>
	<h2>TaskBoard</h2>
	<br />
	<hr />
	<br />
	<TaskBoard columns={columnsData} onFinalUpdate={handleBoardUpdated} />
</div>

<style>
	:global(*) {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}
	h2,
	h5 {
		margin-bottom: 0.4em;
		font-weight: 700;
		font-family: 'Open Sans', sans-serif;
	}
	body {
		background: linear-gradient(to bottom right, #ffa351, #eed971);
	}
	h2 {
		color: #ffbe7b;
	}
	h5 {
		color: #ffa351;
	}
</style>
