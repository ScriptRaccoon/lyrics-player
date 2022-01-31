<script>
    import Lyrics from "./components/Lyrics.svelte";
    import Header from "./components/Header.svelte";
    import Form from "./components/Form.svelte";
    import Player from "./components/Player.svelte";
    let lyrics = "";
    let files = null;
    let currentTime = 0;
    $: lines = lyrics.split("\n").map((line) => {
        const min = parseInt(line.substring(1, 3));
        const sec = parseInt(line.substring(4, 6));
        const text = line.substring(7);
        return {
            time: 60 * min + sec,
            text,
        };
    });
</script>

<main>
    <Header />
    <Form bind:lyrics bind:files />
    <Player {files} />
    <Lyrics {currentTime} {lines} />
</main>
