<script>
    import Lyrics from "./components/Lyrics.svelte";
    import Header from "./components/Header.svelte";
    import Form from "./components/Form.svelte";
    import Player from "./components/Player.svelte";
    import Menu from "./components/Menu.svelte";
    let lyrics = "";
    let files = null;
    let currentTime = 0;
    let lines = [];
    let formVisible = true;
</script>

<Header />
<main>
    <Menu {files} bind:formVisible />
    <Form bind:lyrics bind:lines bind:files {formVisible} />
    <Player {files} bind:currentTime />
    <Lyrics {currentTime} {lines} />
</main>

<style>
    :global(body) {
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        min-height: 100vh;
    }
    main {
        display: flex;
        flex-direction: column;
        height: calc(100vh - 100px);
    }
</style>
