<script>
    export let formVisible;
    export let files;
    $: filename =
        files && files[0] && files[0].name ? files[0].name : "";
</script>

<menu>
    <span class="filename">{filename}</span>
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
</menu>

<style>
    menu {
        display: flex;
        justify-content: space-between;
        padding: 15px 10px;
    }

    input[type="checkbox"] {
        position: absolute;
        visibility: hidden;
    }
    img {
        width: 20px;
        cursor: pointer;
        opacity: 0.7;
    }
    img:hover {
        opacity: 1;
    }
    .filename {
        font-size: 20px;
    }
</style>
