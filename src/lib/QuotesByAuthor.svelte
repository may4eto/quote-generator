<script>
    import Quote from "./Quote.svelte";
    export let quotesByAuthor
</script>

<div>
    <h1>{quotesByAuthor[0].author}</h1>
    {#each quotesByAuthor as quote}
        <Quote>
            {quote.content}
        </Quote>
    {/each}
</div>

<style>
    div {
        max-width: 50vw;
        margin:2rem auto 6rem auto;
    }
    h1 {
        line-height: 1.2;
        margin-bottom: 6rem;
    }

    @media(max-width:768px) {
    div {
        max-width: 66vw;
    }
    @media(max-width:540px) {
    div {
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