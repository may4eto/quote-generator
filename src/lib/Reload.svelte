<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    const onReload = () => {
        dispatch("reload", {})
    }
</script>

<div class="reload" on:click={onReload}>
    <span>random</span>
    <span class="material-symbols-outlined">
        autorenew
    </span>
</div>

<style>
    .reload {
        position: fixed;
        top: 2rem;
        right: 4rem;
        cursor: pointer;
    }
    .reload span {
        font-size: 0.75rem;
    }

    @media(max-width:540px) {
        .reload {
            top: 2rem;
            right: 2rem;
    }
    }
</style>