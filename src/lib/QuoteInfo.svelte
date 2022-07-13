<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    export let randomQuote
    const onSearchQuotesByAuthor = (event) => {
        dispatch("search", {
            text: event.target.childNodes[0].childNodes[0].innerHTML
        })
    }

</script>

<!-- <a href="/"> -->
    <div class="wrapper" on:click = {onSearchQuotesByAuthor}>
        <div class="info">
            <p class="author">{randomQuote.author}</p>
            <p class="tag">{randomQuote.tag}</p>
        </div>
        <span class="material-symbols-outlined">
            arrow_right_alt
        </span>
    </div>
<!-- </a> -->

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
        padding: 2rem 2rem 2rem 4rem;
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
</style>