<div class="btn-group">
  <button class={buttonClass('ALL')} type="button" on:click={showAll}>
    All
  </button>
  <button class={buttonClass('ACTIVE')} type="button" on:click={showActive}>
    Active
  </button>
  <button class={buttonClass('COMPLETED')} type="button" on:click={showCompleted}>
    Completed
  </button>
  <!-- <button class="btn btn__outlined" type="button" on:click={showAll}>
    All
  </button>
  <button class="btn btn__outlined" type="button" on:click={showActive}>
    Active
  </button>
  <button class="btn btn__outlined" type="button" on:click={showCompleted}>
    Completed
  </button> -->
</div>

<script>
  import { createEventDispatcher } from 'svelte';

  export let activeFilter = 'ALL';

  const dispatch = createEventDispatcher();

  function showAll() {
    dispatch('filter', 'ALL');
  }

  function showActive() {
    dispatch('filter', 'ACTIVE');
  }

  function showCompleted() {
    dispatch('filter', 'COMPLETED');
  }

  $: buttonClass = (type) => {
    return 'btn' + (type === activeFilter ? ' btn__filled' : ' btn__outlined');
  }
</script>

<style>
  .btn-group {
    margin-top: 10px;
  }
</style>