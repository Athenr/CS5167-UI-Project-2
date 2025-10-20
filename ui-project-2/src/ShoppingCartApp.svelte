<script>
  import LoginPage from "./screens/LoginPage.svelte";
    import PaymentPage from "./screens/PaymentPage.svelte";
  import ShoppingPage from "./screens/ShoppingPage.svelte";

  let activePage = $state(0)
</script>

<main>
  <div class="main-application-background">
    {#if activePage = 0}
    <LoginPage />
    {:else if activePage = 1}
    <ShoppingPage />
    {:else if activePage = 2}
     <PaymentPage bind:activePage={activePage}/>
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
