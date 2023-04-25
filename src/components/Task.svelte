<script>
	  export let task;
</script>

<style>
  .task {
		    background-color: #f0f0f0;
				border: 1px solid #ccc;
				border-radius: 5px;
				padding: 1rem;
				width: 300px;
	}
</style>

<div class="task">
	<h2>{task.title}</h2>
	<p>{task.description}</p>
</div>


