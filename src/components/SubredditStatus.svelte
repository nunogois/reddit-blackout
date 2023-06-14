<script lang="ts">
  export let subreddit: string;

  const fetchStatus = (async () => {
    const response = await fetch(`https://www.reddit.com/${subreddit}/about.json`)
    return await response.json();
  })()
</script>

{#await fetchStatus}
  <div class='rounded w-12 h-4 animate-pulse bg-neutral-600'></div>
{:then status}
  {#if status.reason === 'private'}
    <span class="text-green-500">Private</span>
  {:else}
    <span class="text-red-500">Open</span>
  {/if}
{:catch error}
  <span class="text-red-500">Error</span>
{/await}