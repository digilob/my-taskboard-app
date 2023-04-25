<script>
	  import { dndzone } from 'svelte-dnd-action';
	  import Task from './Task.svelte';


	  let tasks = [
			    { id: 1, title: 'Task 1', description: 'This is task 1.' },
			    { id: 2, title: 'Task 2', description: 'This is task 2.' },
			    { id: 3, title: 'Task 3', description: 'This is task 3.' },
			  ];
</script>

<style>
	  .task-board {
			    display: flex;
					flex-wrap: wrap;
					gap: 1rem;
		}
</style>


<div class="task-board" use:dndzone={{ items: tasks }}>
	{#each tasks as task (task.id)}
			<Task {task} />
	{/each}
</div>
