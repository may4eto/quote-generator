<script>
    import Quote from "./Quote.svelte";
    export let quotesByAuthor
</script>

<div>
    <h1>{quotesByAuthor[0].author}</h1>
    {#each quotesByAuthor as quote}
        <Quote>
            {quote.text}
        </Quote>
    {/each}
</div>

<style>
    div {
        max-width: 50vw;
        margin:2rem auto 6rem auto;
    }
    h1 {
        margin-bottom: 6rem;
    }
</style>