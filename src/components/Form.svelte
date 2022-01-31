<script>
    export let lyrics = "";
    export let files;
    export let lines;
    let error = "";
    const placeholder =
        "[00:15]There must be some kind of way outta here\n" +
        "[00:19]Said the joker to the thief\n" +
        "[00:23]There's too much confusion\n" +
        "[00:26]I can't get no relief";

    const lineRegExp = /^\[\d{2}:\d{2}\].+$/;

    $: {
        error = "";
        lines = lyrics
            .split("\n")
            .map((line) => {
                if (line.length == 0) return null;
                const match = lineRegExp.test(line);
                if (match) {
                    const min = parseInt(line.substring(1, 3));
                    const sec = parseInt(line.substring(4, 6));
                    const text = line.substring(7);
                    return {
                        time: 60 * min + sec,
                        text,
                    };
                } else {
                    error = `Wrong format: ${line}`;
                    return null;
                }
            })
            .filter((line) => line != null);
    }
</script>

<form on:submit|preventDefault>
    <p>Choose a song file</p>
    <input type="file" accept="audio/*" bind:files />
    <p>Add the lyrics</p>
    <p>Each non-empty line must have the format [mm:ss]text</p>
    <textarea bind:value={lyrics} {placeholder} />
</form>
{#if error}
    <p class="error">
        {error}
    </p>
{/if}

<style>
    textarea {
        width: 100%;
        height: 300px;
        resize: vertical;
    }
    .error {
        padding: 10px 0px;
        color: red;
    }
</style>
