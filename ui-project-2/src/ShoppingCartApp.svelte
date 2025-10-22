<script>
  import LoginPage from "./screens/LoginPage.svelte";
  import PaymentPage from "./screens/PaymentPage.svelte";
  import ShoppingPage from "./screens/ShoppingPage.svelte";
  import StoreMap from "./map/StoreMap.svelte";

  import Cart from "../public/cart.png?url";

  let routeIndex = $state(0);

  let cart = $state([]);

  function next() {
    if (routeIndex < 49) {
      routeIndex++;
    } else {
      currentPage = 2;
    }
  }

  function previous() {
    if (routeIndex > 0) {
      routeIndex--;
    }
  }

  let currentPage = $state(0)
</script>

<main>
  <!-- <StoreMap /> -->
  <div class="main-application-background">
    {#if currentPage == 0}
    <LoginPage bind:currentPage />
    {:else if currentPage == 1}
    <ShoppingPage {routeIndex} bind:cart bind:currentPage />
    {:else if currentPage == 2}
     <PaymentPage bind:activePage={currentPage} {cart}/>
     {:else}
     <LoginPage />
     {/if} 
  </div>
  <div class="controls">
    <button class="primary" onclick={next}>Next Step</button>
    <img src={Cart} alt="Smart Shopping Cart" width="300px">
  </div>
  <!-- TODO: The previous functionality on the map is not working right so I have disabled this button -->
  <!-- <button class="primary" onclick={previous}>Previous</button> -->
</main>

<style>
  .main-application-background {
    width: 1000px;
    height: 750px;
    position: relative;
    background-color: var(--light);
  }

  main {
    display: flex;
    gap: 20px;
  }

  .controls {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
</style>
