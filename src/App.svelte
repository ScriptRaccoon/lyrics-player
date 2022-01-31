<script>
    import Lyrics from "./components/Lyrics.svelte";
    import Header from "./components/Header.svelte";
    import Form from "./components/Form.svelte";
    import Player from "./components/Player.svelte";
    let lyrics = "";
    let files = null;
    let currentTime = 0;
    let lines = [];
</script>

<Header />
<main>
    <Form bind:lyrics bind:lines bind:files />
    <Player {files} bind:currentTime />
    <Lyrics {currentTime} {lines} />
</main>

<style>
    :global(body) {
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    }
    main {
        max-width: 700px;
        margin: 0 auto;
    }
</style>
