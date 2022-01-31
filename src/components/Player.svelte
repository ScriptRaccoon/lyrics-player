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

<style>
    section {
        padding: 20px 0px;
    }
    audio {
        width: 100%;
        height: 30px;
    }
</style>
