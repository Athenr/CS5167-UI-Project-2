<script>
    import { layout } from "./layout";
    import ShelfTile from "./ShelfTile.svelte";

    const width = layout[0].length * 150;
    const height = layout.length * 100;

    let { ...rest } = $props();
</script>

<div {...rest} class={["container", { ...rest.class }]}>
    <!-- TODO: Yes I know this is probably better done as an SVG. 
    This is easier, quicker, and also works though so I am leaving it for now. -->
    <div class="map" style:--width={width} style:--height={height}>
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
                    >
                        <g clip-path="url(#clip0_56_420)">
                            {#if tile.active?.east}
                                <!-- East -->
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
                            {#if tile.active?.west}
                                <!-- West -->
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
                                <circle cx="75" cy="50" r="15" fill="#6585CE" />
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
    }

    .map {
        width: calc(var(--width) * 1px);
        height: calc(var(--height) * 1px);

        background-color: var(--light);

        display: grid;
        grid-template-columns: repeat(calc(var(--width) / 150), 150px);
        grid-template-rows: repeat(calc(var(--height) / 100), 100px);

        /* transform: scale(50%); */
    }

    .tile {
        width: 300px;
        height: 200px;
        box-shadow: inset 0 0 0 5px var(--blue);
    }
</style>
