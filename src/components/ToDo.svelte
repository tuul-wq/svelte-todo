<div class="todo-item">
  {#if isEditState}
    <input class="edit" type="text" bind:value={newTodoValue} bind:this={inputRef}>
    <div class="btn-group">
      <button class="btn btn__outlined" type="button" on:click={cancelEdit}>Cancel</button>
      <button class="btn btn__outlined" type="button" on:click={saveEdit}>Save</button>
    </div>
  {:else}
    <label class="checkbox-group">
      <input
        id={todo.id + '-todo'}
        type="checkbox"
        class="visually-hidden"
        checked={todo.complete}
        on:change={handleCheck}
      >
      <span class="pseudo-checkbox"></span>
      <span class="title" for={todo.id + '-todo'}>{todo.title}</span>
    </label>
    <div class="btn-group">
      <button class="btn btn__outlined" type="button" on:click={toggleEdit}>Edit</button>
      <button class="btn btn__filled danger" type="button" on:click={deleteTodo}>Delete</button>
    </div>
  {/if}
</div>

<script>
  import { createEventDispatcher, tick } from 'svelte';

  export let todo;
  export let index;

  let isEditState = false;
  let inputRef;
  let newTodoValue;

  const dispatch = createEventDispatcher();

  function handleCheck(event) {
    dispatch('checked', { index, checked: event.target.checked });
  }

  async function toggleEdit() {
    isEditState = true;
    newTodoValue = todo.title;

    await tick();
    inputRef.focus();
  }

  function deleteTodo() {
    dispatch('delete', index);
  }

  function cancelEdit() {
    isEditState = false;
  }

  function saveEdit() {
    cancelEdit();
    dispatch('edit', { index, value: newTodoValue });
  }
</script>

<style>
  .checkbox-group {
    display: flex;
    margin-bottom: 10px;
  }

  .title {
    font-size: 18px;
    width: 100%;
    margin-left: 10px;
    line-height: 1;
  }

  .pseudo-checkbox {
    width: 20px;
    height: 20px;
    border-radius: 5px;
    border: 1px solid #474747;
    overflow: hidden;
  }

  .edit {
    font-size:15px;
    width:100%;
    margin-bottom:10px;
    border:1px solid gray;
    padding:6px;
    border-radius: 5px;
  }

  input:focus + .pseudo-checkbox {
    box-shadow: 0 0 0 3px rgb(111, 165, 255);
  }

  input:checked + .pseudo-checkbox::before {
    content: '';
    display: inline-block;
    width: 8px;
    height: 12px;
    border: solid red;
    border-width: 0 3px 3px 0;
    transform: translate(5px, -1px) rotate(45deg);
  }

  .visually-hidden {
    position: absolute;
    clip: rect(0 0 0 0);
    width: 1px;
    height: 1px;
    margin: -1px;
  }
</style>