<script>
  import removeIcon from '$lib/assets/remove.svg';
  let todoList = $state([]);

  let uid = todoList.length + 1;

  function remove(todo) {
		const index = todoList.indexOf(todo);
		todoList.splice(index, 1);
	}
  
</script>

<div class="container mx-auto h-screen py-40 px-10 flex flex-col items-center">
    <div class="form-control">
      <label for="newTodo">Enter your to do:</label>

      <input 
        type="text" 
        id="newTodo" 
        placeholder="Type here" 
        class="input mt-2" 
        onkeydown={(e) => {
          if (e.key !== 'Enter') return; 
          
          if (e.currentTarget.value.trim() !== '') {
            todoList.push({
              id: uid++,
              done: false,
              description: e.currentTarget.value,
            });
  
            e.currentTarget.value = '';
          }
        }}
      />
    </div>

    <div class="todo-list mt-10">
      {#each todoList as todo, i}
        <li class="flex items-center justify-between gap-10">
          <span>{i + 1}. {todo.description}</span>
          <img 
            src={removeIcon} 
            alt="icon" 
            class="w-4 h-4 cursor-pointer"
            onclick={() => remove(todo)}
          />
        </li>
      {/each}
    </div>
</div>

<style>
  li {
    list-style-type: none;
  }
</style>