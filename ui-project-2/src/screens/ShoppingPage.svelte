<script>
    import StoreMap from "../map/StoreMap.svelte";

    const items = [
        {
            id: 0,
            name: "Bananas",
            quantity: 10,
            price: 0.49,
            img: "https://i5.walmartimages.com/seo/Marketside-Fresh-Organic-Bananas-Bunch_f17ef225-0999-4035-9ed1-7a06607333b4.7c3b33492f937bcc19fe3339d5230929.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
        },
        {
            id: 1,
            name: "Tortillas",
            quantity: 1,
            price: 2.78,
            img: "https://i5.walmartimages.com/seo/Mission-Super-Soft-Flour-Tortillas-Soft-Taco-Size-10-Count_059d072a-c60d-493e-9a5c-9175c2849cba.783f703a9193e81b7efe8980cb332508.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
        },
        {
            id: 2,
            name: "Dave's Killer Bread 21 Whole Grains and Seeds Organic Bread Loaf",
            quantity: 1,
            price: 12.45,
            img: "https://i5.walmartimages.com/seo/Dave-s-Killer-Bread-21-Whole-Grains-and-Seeds-Organic-Bread-Loaf-27-oz-Pack-of-9_6c9b0609-3ce6-430a-880e-52d61186e31a.d289021d7c6c7545679f2a1498c52985.jpeg?odnHeight=48&odnWidth=48&odnBg=FFFFFF",
        },
    ];
</script>

<div class="container">
    <div class="pane map">
        <StoreMap class="store-map" />
    </div>
    <div class="pane list">
        <input
            type="search"
            name="search"
            id="search"
            placeholder="Search..."
        />
        <div class="shopping-list">
            {#each items as item}
                <div class="item">
                    <input
                        type="checkbox"
                        name={`item-${item.id}`}
                        id={`item-${item.id}`}
                    />
                    <label for={`item-${item.id}`}>
                        <img src={item.img} alt={item.name} />
                        <div class="name">{item.name}</div>
                        <div class="quantity">x{item.quantity}</div>
                    </label>
                </div>
            {/each}
        </div>
        <button class="primary">Checkout now</button>
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
