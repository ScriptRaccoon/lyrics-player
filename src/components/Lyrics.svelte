<script>
    export let currentTime = 0;
    export let lines = [];
    let lineElements = [];
    const threshold = 0.3;
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
        height: 200px;
        overflow-x: hidden;
        overflow-y: scroll;
        scroll-behavior: smooth;
    }
    .line.selected {
        font-weight: bold;
    }
</style>
