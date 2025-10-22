<script>
  import LoginPage from "./screens/LoginPage.svelte";
  import PaymentPage from "./screens/PaymentPage.svelte";
  import ShoppingPage from "./screens/ShoppingPage.svelte";
  import StoreMap from "./map/StoreMap.svelte";

  let routeIndex = $state(0);

  let cart = $state([]);

  function next() {
    if (routeIndex < 49) {
      routeIndex++;
    } else {
      // TODO: change the page to the checkout
    }
  }

  function previous() {
    if (routeIndex > 0) {
      routeIndex--;
    }
  }
</script>

<main>
  <!-- <StoreMap /> -->
  <div class="main-application-background">
    <!-- <LoginPage /> -->
    <ShoppingPage {routeIndex} bind:cart />
    <!-- <PaymentPage/> -->
  </div>
  <button class="primary" onclick={next}>Next Step</button>
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
</style>
