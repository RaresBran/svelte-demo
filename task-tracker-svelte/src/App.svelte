<script>
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
      placeholder="Adaugă o sarcină..." 
      bind:value={newTask} 
      required
    />
    <button type="submit">Adaugă</button>
  </form>

  {#if tasks.length > 0}
    <ul>
      {#each tasks as task, index}
        <li>
          <input type="checkbox" bind:checked={task.done}>
          <span style: text-decoration={task.done ? 'line-through' : 'none'}>
            {task.name}
          </span>
          <button on:click={() => deleteTask(index)}>Șterge</button>
        </li>
      {/each}
    </ul>
  {:else}
    <p>Nu există sarcini momentan.</p>
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
    gap: 0.5rem;
    margin-bottom: 0.5rem;
  }
  button {
    cursor: pointer;
  }
</style>
