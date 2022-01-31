<script>
    export let lyrics = "";
    export let files;
    const placeholder =
        "[00:15]There must be some kind of way outta here\n" +
        "[00:19]Said the joker to the thief\n" +
        "[00:23]There's too much confusion\n" +
        "[00:26]I can't get no relief";
</script>

<form on:submit|preventDefault>
    <p>Choose a song file</p>
    <input type="file" accept="audio/*" bind:files />
    <p>Add the lyrics</p>
    <p>Each line should have the format [mm:ss]text</p>
    <textarea bind:value={lyrics} {placeholder} />
</form>

<style>
    textarea {
        width: 100%;
        height: 300px;
        resize: vertical;
    }
</style>
