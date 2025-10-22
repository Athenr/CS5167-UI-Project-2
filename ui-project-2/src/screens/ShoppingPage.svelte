<script>
    import StoreMap from "../map/StoreMap.svelte";

    import Straight from "../icons/straight.svg";
    import TurnRight from "../icons/turn_right.svg";
    import TurnLeft from "../icons/turn_left.svg";

    import { layout } from "../map/layout";

    const items = $state([
        {
            id: 0,
            name: "Bananas",
            quantity: 10,
            price: 0.49,
            img: "https://i5.walmartimages.com/seo/Marketside-Fresh-Organic-Bananas-Bunch_f17ef225-0999-4035-9ed1-7a06607333b4.7c3b33492f937bcc19fe3339d5230929.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
        },
        {
            id: 85,
            name: "Tortillas",
            quantity: 1,
            price: 2.78,
            img: "https://i5.walmartimages.com/seo/Mission-Super-Soft-Flour-Tortillas-Soft-Taco-Size-10-Count_059d072a-c60d-493e-9a5c-9175c2849cba.783f703a9193e81b7efe8980cb332508.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
        },
        {
            id: 125,
            name: "Dave's Killer Bread 21 Whole Grains and Seeds Organic Bread Loaf",
            quantity: 1,
            price: 12.45,
            img: "https://i5.walmartimages.com/seo/Dave-s-Killer-Bread-21-Whole-Grains-and-Seeds-Organic-Bread-Loaf-27-oz-Pack-of-9_6c9b0609-3ce6-430a-880e-52d61186e31a.d289021d7c6c7545679f2a1498c52985.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
        },
    ]);

    // const route = [
    //     {
    //         tileId: 121,
    //         direction: {
    //             icon: Straight,
    //             title: "Continue straight",
    //         },
    //     },
    // ];

    let { routeIndex, cart = $bindable(), currentPage = $bindable() } = $props();

    let layoutCopy = $state(structuredClone(layout));
    let directions = $state({});

    function addToCart(e, n) {
        let index = items.findIndex((item) => item.id === n);
        if (e.target.checked) {
            cart.push(items[index]);
        } else {
            let index = cart.findIndex((item) => item.id === n);
            cart.splice(index, 1);
        }
    }

    function getTile(tileId) {
        return layoutCopy[Math.floor(tileId / 12)][tileId % 12];
    }

    let previousIndex = 0;

    $effect(() => {
        const start = 121;
        const end = 130;

        if (routeIndex < previousIndex) {
            let previousTile = getTile(start);

            for (let i = 0; i < previousIndex - 1; i++) {
                previousTile = getTile(previousTile.next);
            }

            Object.assign(
                previousTile,
                layout[Math.floor(previousTile?.tileId / 12)][
                    previousTile?.tileId % 12
                ],
            );
        }
        let tile = getTile(start);
        // TODO: I know this is very inefficient, but I need a quick solution
        for (let i = 0; i < routeIndex; i++) {
            // @ts-ignore
            tile.active = {
                north: false,
                east: false,
                south: false,
                west: false,
            };
            tile = getTile(tile?.next);
        }
        if (tile.previous + 1 === tile.tileId) {
            tile.active.west = false;
        } else if (tile.previous > tile.tileId) {
            tile.active.south = false;
        } else if (tile.previous < tile.tileId) {
            tile.active.north = false;
        }
        tile.active.location = true;

        // TODO: For the sake of time I am just hardcoding this
        if (tile.tileId === 1) {
            directions = {
                icon: "https://i5.walmartimages.com/seo/Marketside-Fresh-Organic-Bananas-Bunch_f17ef225-0999-4035-9ed1-7a06607333b4.7c3b33492f937bcc19fe3339d5230929.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
                title: "Grab 10 bananas",
                subtitle: "From the bottom shelf on the left",
            };
        } else if (tile.tileId === 52) {
            directions = {
                icon: "https://i5.walmartimages.com/seo/Mission-Super-Soft-Flour-Tortillas-Soft-Taco-Size-10-Count_059d072a-c60d-493e-9a5c-9175c2849cba.783f703a9193e81b7efe8980cb332508.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
                title: "Grab 1 pack of tortillas",
                subtitle: "From the middle shelf on the right",
            };
        } else if (tile.tileId === 70) {
            directions = {
                icon: "https://i5.walmartimages.com/seo/Dave-s-Killer-Bread-21-Whole-Grains-and-Seeds-Organic-Bread-Loaf-27-oz-Pack-of-9_6c9b0609-3ce6-430a-880e-52d61186e31a.d289021d7c6c7545679f2a1498c52985.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
                title: "Grab 1 loaf of Dave's Killer Bread",
                subtitle: "From the top shelf on the left",
            };
        } else if ([13, 3, 19, 9].includes(tile.tileId)) {
            directions = {
                icon: TurnRight,
                title: "Turn right",
            };
        } else if ([112, 126].includes(tile.tileId)) {
            directions = {
                icon: TurnLeft,
                title: "Turn left",
            };
        } else {
            directions = {
                icon: Straight,
                title: "Continue straight",
            };
        }

        previousIndex = routeIndex;
    });

    // const route = $derived.by(() => {
    //     const start = 121;
    //     const end = 130;

    //     let route = [{
    //         tileId: start,
    //         direction: {
    //             icon: Straight,
    //             title: "Continue straight",
    //         },
    //     }];
    //     while (route.at(-1)?.tileId !== end) {
    //         const current = route.at(-1);
    //         const tile = getTile(current?.tileId);

    //         route.push({
    //             tileId: tile?.tileId,
    //             direction: {
    //                 icon: Straight,
    //                 title: "Continue straight"
    //             }
    //         })
    //     }

    //     console.log(route);

    //     return route;
    // });
</script>

<div class="container">
    <div class="pane map">
        <StoreMap class="store-map" layout={layoutCopy} {directions} />
    </div>
    <div class="pane list">
        <div class="header">
            <h1 class="no-margin">Grocery List</h1>
            <p class="no-margin">
                Items will automatically be checked off your list below when you
                add them to your cart.
            </p>
        </div>
        <div class="shopping-list">
            {#key cart}
                {#each items as item}
                    <div class="item">
                        <input
                            type="checkbox"
                            name={`item-${item.id}`}
                            id={`item-${item.id}`}
                            onchange={(e) => addToCart(e, item.id)}
                        />
                        <label for={`item-${item.id}`}>
                            <img src={item.img} alt={item.name} />
                            <div class="name">{item.name}</div>
                            <div class="quantity">x{item.quantity}</div>
                        </label>
                    </div>
                {/each}
            {/key}
        </div>
        <button class="primary" onclick={() => currentPage = 2}>Checkout now</button>
    </div>
</div>

<style>
    .container {
        display: flex;
        width: 100%;
        height: 100%;
        align-items: flex-start;
    }

    .pane {
        display: flex;
        padding: 40px;
        flex-direction: column;
        align-items: center;
        gap: 20px;
        flex: 1 0 0;
        align-self: stretch;
    }

    .header {
        display: flex;
        flex-direction: column;
        gap: 20px;
    }

    .map {
        background-color: var(--dark-20);
        width: 50%;

        padding: 0;
    }

    .list {
        align-items: stretch;
        flex-grow: 1;
    }

    .shopping-list {
        flex-grow: 1;
        overflow-y: auto;
    }

    .item {
        display: flex;
        gap: 10px;
        margin-bottom: 10px;

        &:has(:checked) {
            color: var(--dark-50);

            /* TODO: I don't like how this looks when the item name goes to a second line */
            label::after {
                content: "";
                position: absolute;
                height: 1px;
                width: calc(100% - 48px - 10px);
                background-color: var(--dark-50);
                top: 50%;
                left: calc(48px + 10px);
            }
        }

        label {
            display: flex;
            gap: 20px;
            align-items: center;
            flex-grow: 1;

            position: relative;
        }
    }

    .name {
        flex-grow: 1;
    }

    .quantity {
        width: 40px;
        text-align: end;
    }
</style>
