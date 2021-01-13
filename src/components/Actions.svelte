<hr>
<div class="btn-group">
  <button class="btn btn__filled" type="button" on:click={checkAll}>
    Check All
  </button>
  <button class="btn btn__filled" type="button" on:click={removeComplete}>
    Remove Completed
  </button>
</div>

<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  function checkAll() {
    dispatch('checkAll');
  }

  function removeComplete() {
    dispatch('removeComplete');
  }
</script>

<style>

</style>