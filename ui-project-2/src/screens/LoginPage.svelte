<script>
    let { currentPage = $bindable() } = $props();

    function changePage(e) {
        e.preventDefault();
        currentPage = 1;
    }
</script>

<div class="container">
    <div class="import">
        <div class="qr pane" style="cursor: pointer;">
            <h1 class="no-margin">Scan</h1>
            <div class="qr-code" onclick={changePage}></div>
            <p class="instructions no-margin">
                Scan the code above with the Groceries app to import your
                shopping list.
            </p>
        </div>
        <div class="login pane">
            <h1 class="no-margin">Login</h1>
            <p class="instructions no-margin">
                Login to your Groceries account to import your shopping list.
            </p>
            <form class="login-form" action="">
                <input
                    type="text"
                    name="username"
                    id="username"
                    placeholder="Username"
                />
                <input
                    type="password"
                    name="password"
                    id="password"
                    placeholder="Password"
                />
                <button class="primary" onclick={changePage}>Login</button>
                <a href="#" class="forgot-password" onclick={changePage}>Forgot password</a>
            </form>
        </div>
    </div>
    <div class="skip-import">
        <a href="#" onclick={changePage}>No thanks, I just want to start shopping</a>
    </div>
</div>

<style>
    .container {
        display: flex;
        width: 100%;
        height: 100%;
        flex-direction: column;
        align-items: flex-start;
    }

    .import {
        display: flex;
        align-items: center;
        flex: 1 0 0;
        align-self: stretch;
    }

    .skip-import {
        display: flex;
        padding: 20px;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        align-self: stretch;
        border-top: 1px solid var(--dark-20);
    }

    .pane {
        display: flex;
        padding: 40px;
        /* TODO: This number is kind of hacky, it works because we are designing 
        for exactly one screen size, but there is definitely a better way to do this */
        padding-top: 135px;
        flex-direction: column;
        align-items: center;
        gap: 20px;
        flex: 1 0 0;
        align-self: stretch;
    }

    .qr {
        background-color: var(--blue);
        color: var(--light);
    }

    h1 {
        width: 300px;
    }

    .qr-code {
        background-image: url("../../public/sample_qr.svg?url&raw");
        background-size: cover;
        width: 300px;
        height: 300px;

        background-color: var(--light);
        border-radius: 10px;
    }

    .instructions {
        max-width: 300px;
        text-align: start;
    }

    .login-form {
        display: flex;
        flex-direction: column;
        gap: 20px;
        width: 300px;
    }

    .forgot-password {
        text-align: center;
    }
</style>
