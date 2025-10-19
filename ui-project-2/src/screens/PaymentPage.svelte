<script>
    import { formatAsCurrency } from "../utils";

    import Contactless from "../icons/contactless.svg?raw";

    let items = $state([
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
    ]);

    function removeItem(toRemoveID){
        
        items = items.filter(item => item.id !== toRemoveID);
        
    }

    function addItem(name, quantity, price ){
        const newItem = {
            id: items.length,
            name: name,
            quantity: quantity,
            price: price,
            img: "N/A"
        }
        items.push(newItem);
    }
    let name = $state("Item Name");
    let quantity = $state(0);
    let price = $state(0);
</script>

<div class="container">
    <div class="pane receipt">
        <div class="header">
            <h1 class="no-margin">Review</h1>
            <p class="no-margin">Review your final receipt below.</p>
        </div>
        <div class="items">
            {#each items as item}
            
                <div class="item">
                    <button onclick={() => removeItem(item.id)}>X</button>
                    <div class="quantity">{item.quantity}x</div>
                    <div class="name">{item.name}</div>
                    <div class="price number">
                        {formatAsCurrency(item.quantity * item.price)}
                    </div>
                </div>
            {/each}

        </div>
        <div>
                    <input bind:value={name} /><br>Number of Items <input bind:value={quantity}><br>Price Per Item <input type=number bind:value={price}>
                    <br>
            <button onclick={() => addItem(name,quantity,price)}>Add Item</button>
        </div>
        <div class="total">
            <div>
                <p class="total-label no-margin">Total:</p>
                <p class="number no-margin">
                    {formatAsCurrency(
                        items.reduce(
                            (total, item) => total + item.quantity * item.price,
                            0,
                        ),
                    )}
                </p>
            </div>
        </div>
    </div>
    <div class="pane payment">
        <div class="header">
            <h1 class="no-margin">Pay</h1>
            <p class="no-margin">Tap, swipe, or insert your card now to pay.</p>
        </div>
        <div class="payment-prompt">
            <div class="contactless">
                {@html Contactless}
            </div>
        </div>
        <div class="cash">
            <a href="#">I only have cash</a>
        </div>
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
        gap: 20px;
        flex: 1 0 0;
        align-self: stretch;
    }

    .receipt {

        background-color: var(--light);
        color: var(--blue);
    }
    .payment {
        background-color: var(--blue);
        color: var(--light);
    }

    .header {
        background-color: var(--blue);
        color: var(--light);
        text-align: center;
        display: flex;
        flex-direction: column;
        gap: 20px;
        border-radius: 30px;
    }

    .total {
        align-self: stretch;
        display: flex;
        justify-content: end;

        & > div {
            display: flex;
            flex-direction: column;
            gap: 10px;
            width: 150px;
        }

        .number {
            text-align: end;
        }
    }

    .total-label {
        font-weight: 600;
    }

    .number {
        font-style: italic;
    }

    .items {
        display: flex;
        padding: 10px 0;
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
        align-self: stretch;

        flex-grow: 1;
        overflow-y: auto;
    }

    .item {
        display: flex;
        align-items: flex-start;
        gap: 10px;
        align-self: stretch;
    }

    .name {
        flex-grow: 1;
    }

    .quantity {
        min-width: 40px;
    }

    .price {
        min-width: 65px;
        text-align: end;
    }

    .payment-prompt {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        flex-grow: 1;
        gap: 20px;
    }

    .contactless {
        width: 200px;
    }

    .cash {
        text-align: center;
        a {
            color: var(--light);
        }
    }

</style>
