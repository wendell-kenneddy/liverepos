<script lang="ts">
  import type { Repo } from './lib/RepoInfo.svelte';
  import Header from './lib/Header.svelte';
  import SearchBar from './lib/SearchBar.svelte';
  import ErrorMessage from './lib/ErrorMessage.svelte';
  import Loading from './lib/Loading.svelte';
  import RepoList from './lib/RepoList.svelte';

  let promise: Promise<Repo[]>;

  async function fetchRepos(username: string) {
    const res = await fetch(`https://api.github.com/users/${username}/repos`);
    const data = (await res.json()) as Repo[];

    if (res.ok) {
      const reposWithHomepage = data.filter((r) => r.homepage);
      return reposWithHomepage;
    }

    throw new Error('Something went wrong');
  }

  async function handleSearch(e: CustomEvent<{ username: string }>) {
    promise = fetchRepos(e.detail.username);
  }
</script>

<Header />

<main>
  <SearchBar on:search={handleSearch} />

  {#if promise}
    {#await promise}
      <Loading />
    {:then repos}
      <RepoList {repos} />
    {:catch}
      <ErrorMessage />
    {/await}
  {/if}
</main>

<style>
  main {
    width: 90vw;
    max-width: 720px;
    margin: 2rem auto;
  }
</style>
