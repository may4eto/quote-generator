<script>
  import { onMount } from 'svelte'
  import Footer from "./lib/Footer.svelte"
  import axios from 'axios'
  import Quote from './lib/Quote.svelte'
  import Button from './lib/Button.svelte'
  import QuoteInfo from './lib/QuoteInfo.svelte';
  import QuotesByAuthor from './lib/QuotesByAuthor.svelte'

  let randomQuote = {}
  let quotesByAuthor = []
  const url = "https://api.quotable.io/"
  const fetchQuote = async() => await axios.get(url + "random", {
    headers: {"Access-Control-Allow-Origin": "*"}
  })
      .then(function (response) {
	      randomQuote = response.data;
      })
      .catch(function (error) {
	      alert("Sorry, something is wrong :disappointed: Please try again later.)
      });
  const fetchQuotesByAuthor = async(author) => await axios.get(url + "quotes?author=" + author.toLowerCase().replaceAll(' ', '-'), {
    headers: {"Access-Control-Allow-Origin": "*"}
  })
      .then(function (response) {
        quotesByAuthor = [...response.data.results]
      })
      .catch(function (error) {
	alert("Sorry, something is wrong :disappointed: Please try again later.)
      });
  onMount(async() => {
     fetchQuote()
  })
  const reloadQuote = () => {
    if (quotesByAuthor.length > 0) {
      quotesByAuthor.length = 0
    } else {
      fetchQuote()
    }
  }
  const searchQuotesByAuthor = (event) => {
    fetchQuotesByAuthor(event.detail.text)
  }
</script>

<main>
    <Button {quotesByAuthor} on:reload= {reloadQuote}/>
  {#if randomQuote.content}
    {#if quotesByAuthor.length === 0} 
      <div class="home">
        <div>
          <Quote>{randomQuote.content}</Quote>
          <QuoteInfo {randomQuote} on:search={searchQuotesByAuthor} />
        </div>
      </div>
    {:else}
      <QuotesByAuthor {quotesByAuthor}/>
    {/if}
  {:else}
    <div class="home">
      <p>loading...</p>
    </div>
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
