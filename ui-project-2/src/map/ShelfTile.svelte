<script>
    let { selected = -1, reverse = false } = $props();
</script>

<div class={["tile", { active: selected != -1, reversed: reverse }]}>
    <div class={["shelf", { selected: selected === 2 }]}></div>
    <div class={["shelf", { selected: selected === 1 }]}></div>
    <div class={["shelf", { selected: selected === 0 }]}></div>
</div>

<style>
    .tile {
        width: 150px;
        height: 100px;

        display: flex;
        flex-direction: row;

        background-color: var(--dark-20);
    }

    .shelf {
        flex-grow: 1;
    }

    .active .shelf {
        border: 1px solid var(--dark-50);
    }

    .shelf.selected {
        border: 5px solid var(--blue);
        background-color: var(--blue-20);
    }

    .reversed {
        flex-direction: row-reverse;
    }
</style>
