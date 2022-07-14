<script>
  import { onMount } from 'svelte'
  import Footer from "./lib/Footer.svelte"
  import axios from 'axios'
  import Quote from './lib/Quote.svelte'
  import Reload from './lib/Reload.svelte'
  import QuoteInfo from './lib/QuoteInfo.svelte';
  import QuotesByAuthor from './lib/QuotesByAuthor.svelte'

  let randomQuote = {}
  let quotesByAuthor = []
  const url = "https://goquotes-api.herokuapp.com/api/v1/"
  const fetchQuote = async() => await axios.get(url + "random?count=1")
      .then(function (response) {
        quotesByAuthor.length = 0
	      randomQuote = response.data.quotes[0];
        console.log(randomQuote)
      })
      .catch(function (error) {
	      console.error(error);
      });
  const fetchQuotesByAuthor = async(author) => await axios.get(url + "all?type=author&val=" + author)
      .then(function (response) {
        quotesByAuthor = [...response.data.quotes]
        console.log(quotesByAuthor)
      })
      .catch(function (error) {
	      console.error(error);
      });
  onMount(async() => {
     fetchQuote()
  })
  const reloadQuote = () => {
    fetchQuote()
  }
  const searchQuotesByAuthor = (event) => {
    fetchQuotesByAuthor(event.detail.text)
  }
</script>

<main>
    <Reload on:reload= {reloadQuote}/>
  {#if randomQuote.text}
    {#if quotesByAuthor.length === 0} 
      <div class="home">
        <div>
          <Quote>{randomQuote.text}</Quote>
          <QuoteInfo {randomQuote} on:search={searchQuotesByAuthor} />
        </div>
      </div>
    {:else}
      <QuotesByAuthor {quotesByAuthor}/>
    {/if}
  {:else}
    <p>loading...</p>
  {/if}
</main>
<Footer />

<style>
  .home {
    min-height: 100vh;
    display: flex;
    align-items:center;
    justify-content: center;
    margin-bottom: 2rem;
  }

</style>
