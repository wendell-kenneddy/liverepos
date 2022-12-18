<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher<{ search: { username: string } }>();
  let username: string = '';

  function triggerSearch() {
    if (!username.length) return;

    dispatch('search', {
      username,
    });
  }
</script>

<form class="container" on:submit|preventDefault={triggerSearch}>
  <label for="username">User</label>
  <input
    type="text"
    name="username"
    id="username"
    placeholder="wendell-kenneddy"
    bind:value={username}
  />

  <button type="submit">Search</button>
</form>

<style>
  .container {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
  }

  label {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border-width: 0;
  }

  input {
    border: none;
    border-radius: 4px;
    padding: 0.5rem;
    width: 70%;
    color: rgba(0, 0, 0, 0.87);
    box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
  }

  input:focus {
    outline-style: solid;
    outline-color: #1976d2;
    outline-width: 2px;
  }

  button {
    background-color: #1976d2;
    border: none;
    border-radius: 4px;
    padding: 0.5rem;
    width: 30%;
    font-size: 0.875rem;
    text-transform: uppercase;
    font-weight: 600;
    color: #fff;
    cursor: pointer;
    transition: filter 0.2s ease-in-out;
  }

  button:focus {
    outline-style: solid;
    outline-offset: 2px;
    outline-color: #1976d2;
    outline-width: 2px;
  }

  button:hover {
    filter: brightness(0.9);
  }
</style>
