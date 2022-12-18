<script lang="ts">
  import RepoInfo, { type Repo } from './RepoInfo.svelte';

  export let repos: Repo[];
</script>

<ul class="container">
  {#each repos as repo (repo.id)}
    <RepoInfo {repo} />
  {/each}
</ul>

<style>
  .container {
    margin: 1rem 0;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }
</style>
