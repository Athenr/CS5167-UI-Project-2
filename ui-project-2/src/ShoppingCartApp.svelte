<script>
  import LoginPage from "./screens/LoginPage.svelte";
    import PaymentPage from "./screens/PaymentPage.svelte";
  import ShoppingPage from "./screens/ShoppingPage.svelte";

  let currentPage = $state(0)
</script>

<main>
  <div class="main-application-background">
    {#if currentPage == 0}
    <LoginPage on:gotoShopping={() => currentPage = 1} />
    {:else if currentPage == 1}
    <ShoppingPage />
    {:else if currentPage == 2}
     <PaymentPage bind:activePage={currentPage}/>
     {:else}
     <LoginPage />
     {/if} 
  </div>
</main>

<style>
  .main-application-background {
    width: 1000px;
    height: 750px;
    position: relative;
    background-color: var(--light);
  }
</style>
