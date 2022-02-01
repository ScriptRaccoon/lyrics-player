<script>
    export let currentTime = 0;
    export let lines = [];
    let lineElements = [];
    const threshold = 0.5;
    let currentIndex = 0;
    // TODO: update currentIndex less often
    $: {
        currentIndex = lines.findIndex(
            (line, index) =>
                currentTime + threshold >= line.time &&
                (index == lines.length - 1 ||
                    currentTime + threshold < lines[index + 1].time)
        );
    }
    $: if (currentIndex >= 0) {
        lineElements[currentIndex].scrollIntoView({
            block: "center",
        });
    }
</script>

<section>
    {#each lines as line, index}
        <p
            class="line"
            class:selected={currentIndex == index}
            bind:this={lineElements[index]}
        >
            {line.text}
        </p>
    {/each}
</section>

<style>
    section {
        flex-grow: 1;
        overflow-x: hidden;
        overflow-y: scroll;
        scroll-behavior: smooth;
        padding: 0px 10px;
    }
    .line {
        color: #aaa;
        transition: color 150ms linear;
        text-align: center;
        font-size: min(50px, 6vw);
        line-height: 1.5;
        margin: 20px 0px;
    }
    .line.selected {
        color: #000;
    }
</style>
