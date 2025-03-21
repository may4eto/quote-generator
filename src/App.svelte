<script>
  // @ts-nocheck
  
  import { onMount } from 'svelte';
  import Footer from './lib/Footer.svelte';
  import axios from 'axios';
  import Quote from './lib/Quote.svelte';
  import Button from './lib/Button.svelte';
  import QuoteInfo from './lib/QuoteInfo.svelte';
  import QuotesByAuthor from './lib/QuotesByAuthor.svelte';
  import { error } from '@sveltejs/kit';
  
  let randomQuote = {};
  let quotesByAuthor = [];
  let isLoading = false; // Add a loading state
  
  function isEmpty(obj) {
    return Object.keys(obj).length === 0;
  }
  
  const url = 'https://thequoteshub.com/api/';
  
  const fetchQuote = async () => {
    isLoading = true; // Set loading to true before the API call
    try {
      const response = await axios.get(url, {
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Accept": "application/json"
        }
      });
      randomQuote = response.data; // Update randomQuote with the first quote
      isLoading = false; // Set loading to false after data is fetched
    } catch (err) {
      error(503, 'Sorry, wisdom seeker, there is a problem with the service... Please try again later.');
    } finally {
    isLoading = false; // Set loading to false after the API call completes
  }
  };
  
  const fetchQuotesByAuthor = async (author) => {
    isLoading = true; // Set loading to true before the API call
    try {
      const response = await axios.get(url + '/authors/' + author, {
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Accept": "application/json"
        }
      });
      quotesByAuthor = [...response.data?.quotes]; // Update quotesByAuthor with the fetched quotes
    } catch (err) {
      error(503, 'Sorry, wisdom seeker, there is a problem with the service... Please try again later.');
    } finally {
    isLoading = false; // Set loading to false after the API call completes
  }
  };
  
  onMount(async () => {
    await fetchQuote(); // Fetch the initial quote when the component mounts
  });
  
  const reloadQuote = () => {
    if (quotesByAuthor.length > 0) {
      quotesByAuthor = []; // Reset quotesByAuthor
    } else {
      fetchQuote(); // Fetch a new random quote
    }
  };
  
  const searchQuotesByAuthor = (event) => {
    fetchQuotesByAuthor(event.detail.text).replace(/ /g, '+'); // Fetch quotes by author
  };
  </script>
  
  <main>
    <Button {quotesByAuthor} on:reload={reloadQuote} />
    {#if isLoading}
      <div class="home">
        <p>loading...</p>
      </div>
    {:else}
      {#if !isEmpty(randomQuote)}
        {#if quotesByAuthor.length === 0}
          <div class="home">
            <div>
              <Quote {randomQuote} />
              <QuoteInfo {randomQuote} on:search={searchQuotesByAuthor} />
            </div>
          </div>
        {:else}
          <QuotesByAuthor {quotesByAuthor} />
        {/if}
      {/if}
    {/if}
  </main>
  
  <Footer />
  
  <style>
    .home {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 2rem;
    }
    .error {
      max-width: 50%;
      margin-left: auto;
      margin-right: auto;
    }
    @media (max-width: 720px) {
      .error {
        max-width: 80%;
      }
    }
  </style>
