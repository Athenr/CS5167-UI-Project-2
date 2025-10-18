<script>
  import LoginPage from "./screens/LoginPage.svelte";
    import PaymentPage from "./screens/PaymentPage.svelte";
  import ShoppingPage from "./screens/ShoppingPage.svelte";
</script>

<main>
  <div class="main-application-background">
    <LoginPage />
    <!-- <ShoppingPage /> -->
     <!-- <PaymentPage/> -->
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
