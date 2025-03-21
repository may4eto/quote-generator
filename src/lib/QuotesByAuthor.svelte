<script>
    import Quote from "./Quote.svelte";
    export let quotesByAuthor = []
</script>

{#if quotesByAuthor.length > 0}
  <div class="quotes-list">
    <h1>{quotesByAuthor[0].author}</h1>
    {#each quotesByAuthor.slice(0, 8) as quote}
        <Quote randomQuote={quote} />
    {/each}
  </div>
{:else}
  <p>No quotes found for this author.</p>
{/if}

<style>
    div.quotes-list {
        max-width: 50vw;
        margin:2rem auto 6rem auto;
    }
    h1 {
        line-height: 1.2;
        margin-bottom: 6rem;
    }

    @media(max-width:768px) {
    div.quotes-list {
        max-width: 66vw;
    }
    @media(max-width:540px) {
    div.quotes-list {
        max-width: 100vw;
    }
    h1 {
        max-width: 50%;
        padding: 0 1rem;
        margin-bottom: 4rem;
    }
  }
  }
</style>