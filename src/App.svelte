<script>
  import { fade } from 'svelte/transition';
  let newTask = "";
  let tasks = [];

  function addTask() {
    if (newTask.trim() !== "") {
      tasks = [...tasks, { name: newTask, done: false }];
      newTask = "";
    }
  }

  function deleteTask(index) {
    tasks = tasks.filter((_, i) => i !== index);
  }
</script>

<main>
  <h1>Task Tracker</h1>
  
  <form on:submit|preventDefault={addTask}>
    <input 
      placeholder="Add a task..." 
      bind:value={newTask} 
      required
    />
    <button type="submit">Add</button>
  </form>

  {#if tasks.length > 0}
    <ul>
      {#each tasks as task, index (task.name)}
        <li transition:fade>
          <input type="checkbox" bind:checked={task.done}>
          <span style:text-decoration={task.done ? 'line-through' : 'none'}>
            {task.name}
          </span>
          <button on:click={() => deleteTask(index)}>Remove</button>
        </li>
      {/each}
    </ul>  
  {:else}
    <p>No tasks for now.</p>
  {/if}
</main>

<style>
  main {
    max-width: 500px;
    margin: 2rem auto;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 8px;
  }
  form {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
  }
  input[type="text"], button {
    padding: 0.5rem;
    font-size: 1rem;
  }
  ul {
    list-style: none;
    padding: 0;
  }
  li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0.5rem;
  }

  form input {
    width: 100%;
  }

  li span {
    flex: 1;
  }

  button {
    cursor: pointer;
  }
</style>
