<script>
    import { onMount } from "svelte";

    let circle;

    onMount(() => {
        if (circle) {
            circle.scrollIntoView({ behavior: "smooth", block: "center", inline: "center" });
        }
    });
</script>

<circle cx="75" cy="50" r="15" fill="#6585CE" bind:this={circle} />
