<script>
  // Define the randomQuote prop
  export let randomQuote = {};
</script>

<div class="quote">
  <blockquote>
    <!-- Render the quote text from the randomQuote prop -->
    {randomQuote.text}
  </blockquote>
</div>

<style>
  .quote {
    max-width: 50vw;
    margin-bottom: 2rem;
  }
  blockquote {
    font-size: 1.5rem;
    border-left: solid 0.25rem var(--accent);
    padding-left: 4rem;
    margin: 0 0 2rem 0;
  }
  blockquote::before {
    content: '\201C';
  }
  blockquote::after {
    content: '\201D';
  }
  .author {
    text-align: right;
    font-style: italic;
    color: var(--text-secondary);
  }

  @media (max-width: 768px) {
    .quote {
      max-width: 75vw;
    }
  }
  @media (max-width: 540px) {
    .quote {
      max-width: 100vw;
      padding: 0 1rem;
    }
    blockquote {
      padding-left: 2rem;
    }
  }
</style>
