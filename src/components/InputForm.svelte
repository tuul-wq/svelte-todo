<form class="form" on:submit|preventDefault={addNewTodo}>
  <label class="title" for="form-input">What needs to be done?</label>
  <input
    id="form-input"
    class="input"
    type="text"
    autocomplete="off"
    bind:this={inputRef}
    on:input={handleInput}
    >
  <button class="btn btn__filled" type="submit" disabled bind:this={btnRef}>Add new todo</button>
</form>

<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  let inputValue = '';
  let inputRef;
  let btnRef;

  function handleInput(event) {
    inputValue = event.target.value;
    btnRef.disabled = !inputValue;
  }

  function addNewTodo() {
    dispatch('addTodo', inputValue);

    inputValue = '';
    inputRef.blur();
    inputRef.value = '';
    btnRef.disabled = true;
  }
</script>

<style>
  .form {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .title {
    font-size: 18px;
    margin-bottom: 15px;
  }

  .input {
    width: 100%;
    border: 1px solid gray;
    padding: 10px;
    font-size: 15px;
    margin-bottom: 10px;
  }

  .btn:disabled {
    cursor: default;
    background-color: #9b9b9b;
  }
</style>