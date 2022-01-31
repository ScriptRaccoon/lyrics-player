<script>
    export let currentTime = 0;
    export let files;
    $: file = files ? files[0] : null;
</script>

{#if file}
    <section>
        <audio
            src={URL.createObjectURL(file)}
            bind:currentTime
            controls
        />
    </section>
{/if}
