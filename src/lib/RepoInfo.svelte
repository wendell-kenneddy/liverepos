<script lang="ts" context="module">
  export interface Repo {
    name: string;
    id: number;
    description?: string;
    homepage?: string;
  }
</script>

<script lang="ts">
  export let repo: Repo;

  const formattedUrl = repo.homepage.includes('https://')
    ? repo.homepage
    : `https://${repo.homepage}`;
</script>

<a
  class="container"
  href={formattedUrl}
  rel="noopener noreferrer"
  target="_blank"
>
  <span>{repo.name}</span>
  <p>{repo.description ?? 'No description :('}</p>
</a>

<style>
  .container {
    background: #fff;
    border-radius: 4px;
    width: 100%;
    padding: 0.5rem;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 0.4rem;
    text-decoration: none;
    box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05);
    transition: color 0.2s;
  }

  .container:focus {
    outline-style: solid;
    outline-color: #1976d2;
    outline-width: 2px;
  }

  span {
    color: #1976d2;
    font-weight: 500;
  }

  p {
    font-size: 0.875rem;
    color: rgba(0, 0, 0, 0.67);
  }

  .container:hover p {
    color: rgba(0, 0, 0, 0.87);
  }
</style>
