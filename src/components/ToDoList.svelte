<ul class="todo-list">
  {#each todoList as todo, index (todo.id)}
    <li>
      <ToDo
        {todo}
        {index}
        on:checked={handleChecked}
        on:edit={handleEdit}
        on:delete={handleDelete}
      />
    </li>
  {:else}
    <li>Nothing to do here</li>
  {/each}
</ul>

<script>
  import ToDo from './ToDo.svelte';
  import { createEventDispatcher } from 'svelte';

  export let todoList = [];

  const dispatch = createEventDispatcher();

  function handleChecked({ detail: { index, checked } }) {
    dispatch('checked', { index, checked });
  }

  function handleEdit({ detail: { index, value } }) {
    dispatch('edit', { index, value });
  }

  function handleDelete({ detail: index }) {
    dispatch('delete', index);
  }
</script>

<style>
  .todo-list {
    list-style: none;
    padding: 0;
  }

  .todo-list li + li {
    margin-top: 20px;
  }
</style>