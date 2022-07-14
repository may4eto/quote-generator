<script>
</script>

<div class="quote">
    <blockquote>
      <slot></slot>
    </blockquote>
</div>

<style>
  .quote {
    max-width: 50vw;
    margin-bottom: 2rem;
  }
  blockquote {
    font-size: 1.5rem;
    border-left: solid 4px var(--accent);
    padding-left: 4rem;
    margin: 0 0 2rem 0;
  }
  blockquote::before {
    content: '\201C';
  }
  blockquote::after {
    content: '\201D';
  }
</style>
