<script>
    import { onMount } from "svelte";
    import ShelfTile from "./ShelfTile.svelte";
    import LocationDot from "./LocationDot.svelte";

    let { route = $bindable(), layout, directions, ...rest } = $props();

    const width = layout[0].length * 150;
    const height = layout.length * 100;

    let container;
    let circle;

    onMount(() => {
        if (container) {
            container.scrollTop = container.scrollHeight;
        }
    });

    let isScrolling = false;
    let position = $state({ x: 0, y: 0 });

    function startScrolling(e) {
        isScrolling = true;
        position.x = e.clientX;
        position.y = e.clientY;
        e.preventDefault();
    }

    function stopScrolling() {
        isScrolling = false;
    }

    function scroll(e) {
        if (isScrolling) {
            container.scrollTop -= e.clientY - position.y;
            container.scrollLeft -= e.clientX - position.x;

            position.x = e.clientX;
            position.y = e.clientY;
        }
    }
</script>

<svelte:window onmousemove={scroll} onmouseup={stopScrolling} />
<div {...rest} class={["container", { ...rest.class }]} bind:this={container}>
    <div class="directions">
        <div class="icon">
            <img src={directions.icon} alt={directions.title} />
        </div>
        <div class="text">
            <div class="main">{directions.title}</div>
            {#if directions.subtitle}
                <p class="no-margin">{directions.subtitle}</p>
            {/if}
        </div>
    </div>
    <!-- TODO: Yes I know this is probably better done as an SVG. 
    This is easier, quicker, and also works though so I am leaving it for now. -->

    <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div
        class="map"
        style:--width={width}
        style:--height={height}
        onmousedown={startScrolling}
        onmousemove={scroll}
    >
        {#each layout as row}
            {#each row as tile}
                {#if tile.type === "shelf"}
                    <ShelfTile
                        selected={tile.selected}
                        reverse={tile.reversed}
                    />
                {:else}
                    <svg
                        width="150"
                        height="100"
                        viewBox="0 0 150 100"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                        id="p{tile.tileId}"
                    >
                        <g clip-path="url(#clip0_56_420)">
                            {#if tile.active?.west}
                                <!-- West -->
                                <path
                                    d="M0 50L82.5 50"
                                    stroke="#6585CE"
                                    stroke-width="15"
                                />
                            {/if}
                            {#if tile.active?.south}
                                <!-- South -->
                                <path
                                    d="M75 42.5L75 100"
                                    stroke="#6585CE"
                                    stroke-width="15"
                                />
                            {/if}
                            {#if tile.active?.east}
                                <!-- East -->
                                <path
                                    d="M67.5 50L150 50"
                                    stroke="#6585CE"
                                    stroke-width="15"
                                />
                            {/if}
                            {#if tile.active?.north}
                                <!-- North -->
                                <path
                                    d="M75 0L75 57.5"
                                    stroke="#6585CE"
                                    stroke-width="15"
                                />
                            {/if}
                            {#if tile.active?.location}
                                <!-- Location -->
                                <LocationDot />
                            {/if}
                        </g>
                        <defs>
                            <clipPath id="clip0_56_420">
                                <rect width="150" height="100" fill="white" />
                            </clipPath>
                        </defs>
                    </svg>
                {/if}
            {/each}
        {/each}
    </div>
</div>

<style>
    .container {
        overflow: auto;
        max-width: 100%;

        scrollbar-width: none;

        position: relative;
        background-color: var(--dark-50);
    }

    .map {
        width: calc(var(--width) * 1px);
        height: calc(var(--height) * 1px);

        background-color: var(--dark-10);

        display: grid;
        grid-template-columns: repeat(calc(var(--width) / 150), 150px);
        grid-template-rows: repeat(calc(var(--height) / 100), 100px);

        margin-top: 100px;
    }

    .directions {
        /* TODO: This should probably not be in px, but it works since this is for a specific screen size */
        width: 440px;
        height: 60px;
        /* TODO: This is also a little hacky */
        margin-top: 10px;
        margin-left: 10px;

        position: fixed;
        background-color: var(--light);

        color: var(--dark);

        display: flex;
        padding: 10px 20px;

        gap: 20px;

        border-radius: 5px;
    }

    .icon {
        display: flex;

        align-items: center;
    }

    .text {
        display: flex;

        justify-content: center;

        flex-direction: column;

        gap: 5px;

        .main {
            font-weight: 600;
        }
    }
</style>
