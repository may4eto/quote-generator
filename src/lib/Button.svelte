<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    const onReload = () => {
        dispatch("reload", {})
    }
    export let quotesByAuthor
</script>

<div class="reload" on:click={onReload}>
    {#if quotesByAuthor.length === 0}
    <span>random</span>
    <span class="material-symbols-outlined">
        autorenew
    </span>
    {:else}
    <span class="material-symbols-outlined">
        arrow_back
    </span>
    <span>back</span>
    {/if}
</div>

<style>
    .reload {
        display: flex;
        align-items: center;
        position: fixed;
        top: 2rem;
        right: 4rem;
        cursor: pointer;
    }
    .reload span {
        font-size: 0.75rem;
        display: inline-block;
    }
    .reload span:first-child {
        margin-right: 0.25rem;
    }

    @media(max-width:540px) {
        .reload {
            top: 2rem;
            right: 2rem;
    }
    }
</style>