<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
  
    export let randomQuote;
  
    const onSearchQuotesByAuthor = () => {
      // Dispatch the "search" event with the author's name as the payload
      dispatch('search', {
        text: randomQuote.author_id,
      });
    };
  </script>
  
  <div class="wrapper" on:click={onSearchQuotesByAuthor}>
    <div class="info">
      <p class="author">{randomQuote.author}</p>
      <p class="tag">
        {#if randomQuote.tags?.length > 0}
            {#each randomQuote.tags as tag}
                <span>{tag}</span>
            {/each}
        {/if}
      </p>
    </div>
    <span class="material-symbols-outlined">arrow_right_alt</span>
  </div>


<style>
    /* a {
        text-decoration: none;
    } */
    div.wrapper:hover  {
        background-color: var(--dark-grey);
        cursor: pointer;
    }
    div.wrapper:hover span {
        display: block;
    }
    div.wrapper:hover div.info p,
    div.wrapper:hover  span {
        color: var(--white);
    }
    div.wrapper {
        padding: 1rem 1rem 1rem 4rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    div.wrapper span {
        display: none;
    }
    div.info p {
        margin: 0.33rem 0;
    }
    div.info p.author {
        font-weight: 700;
        color: var(--middle-grey);
     }
    div.info p.tag {
        font-size: 0.6rem;
        color: var(--light-grey);
    }
    div.info p.tag span {
        display: inline;
        margin-right: 0.5rem;
    }
  @media(max-width: 540px) {
    div.wrapper {
        padding: 1rem 1rem 1rem 2rem;
        margin: 0 1rem;
    }
  }
</style>