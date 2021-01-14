<ul class="todo-list">
  {#each todoList as todo, index (todo.id)}
    <li>
      <ToDo {todo} {index} on:checked on:delete on:edit />
    </li>
  {:else}
    <li class="none">Nothing to do here 🥳</li>
  {/each}
</ul>

<script>
  import ToDo from './ToDo.svelte';

  export let todoList = [];
</script>

<style>
  .todo-list {
    list-style: none;
    padding: 0;
    margin: 35px 0;
  }

  .todo-list li + li {
    margin-top: 20px;
  }

  .none {
    font-size: 18px;
  }
</style>