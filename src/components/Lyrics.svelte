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
    <div class="lines">
        {#each lines as line, index}
            <p
                class="line"
                class:selected={currentIndex == index}
                bind:this={lineElements[index]}
            >
                {line.text}
            </p>
        {/each}
    </div>

    <div class="overlay" />
</section>

<style>
    .lines {
        position: absolute;
        inset: 0;
    }
    section {
        flex-grow: 1;
        overflow-x: hidden;
        overflow-y: scroll;
        scroll-behavior: smooth;
        position: relative;
    }
    .overlay {
        position: sticky;
        inset: 0;
        height: 100%;
        z-index: 100;
        background: linear-gradient(
            white 0%,
            transparent 15%,
            transparent 85%,
            white 100%
        );
    }
    .line {
        color: #aaa;
        transition: color 150ms linear;
        text-align: center;
        font-size: min(50px, 6vw);
        line-height: 1.5;
        margin: 20px 10px;
    }
    .line.selected {
        color: #000;
    }
    .line:first-of-type {
        margin-top: 20vh;
    }
    .line:last-of-type {
        margin-bottom: 20vh;
    }
</style>
