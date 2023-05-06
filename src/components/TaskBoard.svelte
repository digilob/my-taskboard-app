<script>
	import Task from './Task.svelte';
	import { dndzone } from 'svelte-dnd-action';

	let tasks = [
		{ id: 1, title: 'Task 1', description: 'This is task 1.', status: 'TODO' },
		{ id: 2, title: 'Task 2', description: 'This is task 2.', status: 'TODO' },
		{ id: 3, title: 'Task 3', description: 'This is task 3.', status: 'TODO' }
	];

	const flipDurationMs = 300;

	function handleDndConsider(e) {
		tasks = e.detail.items;
	}

	function handleDndFinalize(e) {
		tasks = e.detail.items;
	}
</script>

<div
	class="task-board"
	use:dndzone={{ items: tasks, flipDurationMs }}
	on:consider={handleDndConsider}
	on:finalize={handleDndFinalize}
>
	<div class="task-list todo">
		<h2>TODO</h2>
		{#each tasks.filter((t) => t.status === 'TODO') as task (task.id)}
			<Task {task} />
		{/each}
	</div>
	<div class="task-list in-dev">
		<h2>In Development</h2>
		{#each tasks.filter((t) => t.status === 'INDEV') as task (task.id)}
			<Task {task} />
		{/each}
	</div>
	<div class="task-list done">
		<h2>DONE</h2>
		{#each tasks.filter((t) => t.status === 'DONE') as task (task.id)}
			<Task {task} />
		{/each}
	</div>
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
		background: linear-gradient(to bottom right, #f76d6d, #ff9c9c);
	}

	.task-list.in-dev {
		background: linear-gradient(to bottom right, #6dd5f7, #9ccfff);
	}

	.task-list.done {
		background: linear-gradient(to bottom right, #f7d66d, #ffc99c);
	}
</style>
