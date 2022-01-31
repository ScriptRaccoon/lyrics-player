<script>
    import { slide, fade } from "svelte/transition";
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

    let formVisible = true;
</script>

<section>
    <div class="controls">
        <span class="filename">
            {files && files[0] && files[0].name ? files[0].name : ""}
        </span>
        <label for="formCheck">
            <img
                src={formVisible
                    ? "./icons/hide.png"
                    : "./icons/show.png"}
                alt="toggle form"
            />
        </label>
        <input
            type="checkbox"
            id="formCheck"
            bind:checked={formVisible}
        />
    </div>

    {#if formVisible}
        <form transition:slide on:submit|preventDefault>
            <label for="fileInput">Choose a song from your PC</label>
            <input
                id="fileInput"
                type="file"
                accept="audio/*"
                bind:files
            />
            <p class="relative">
                <label for="lyricsInput">Paste the lyrics</label>
            </p>

            <p class="hint">
                Each non-empty line must have the format [mm:ss]text.
            </p>
            <textarea
                id="lyricsInput"
                bind:value={lyrics}
                {placeholder}
            />
        </form>
        {#if error}
            <p transition:fade={{ duration: 150 }} class="error">
                {error}
            </p>
        {/if}
    {/if}
</section>

<style>
    input,
    label,
    textarea {
        display: block;
    }
    label {
        font-weight: bold;
        font-size: 20px;
        margin-bottom: 5px;
    }
    textarea {
        width: 100%;
        height: 100px;
        resize: vertical;
        padding: 5px;
        font-size: 12px;
        outline: none;
        border-radius: 4px;
        border: 1px solid #555;
        opacity: 0.8;
        transition: background-color 100ms linear,
            opacity 100ms linear;
    }
    textarea:focus {
        border: 1px solid var(--primary-color);
        background-color: #efeff5;
        opacity: 1;
    }
    .hint {
        color: #444;
        margin-bottom: 5px;
    }
    .error {
        margin: 10px 0px;
        color: red;
    }
    input[type="file"] {
        width: 50%;
        margin-bottom: 20px;
    }
    .controls {
        display: flex;
        justify-content: space-between;
        padding: 10px 0px;
    }

    input[type="checkbox"] {
        position: absolute;
        visibility: hidden;
    }
    .controls label img {
        margin-right: 10px;
        width: 20px;
        cursor: pointer;
        opacity: 0.7;
    }
    .controls label img:hover {
        opacity: 1;
    }
    .filename {
        font-size: 20px;
    }
</style>
