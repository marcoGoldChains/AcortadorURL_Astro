<script>
    import { onMount } from 'svelte';
    export let urlResults

    let textarea;

    onMount(() => {
        textarea.select();
        document.execCommand('copy');
    })
</script>


<textarea bind:value={urlResults} bind:this={textarea} id="clipboard"></textarea>