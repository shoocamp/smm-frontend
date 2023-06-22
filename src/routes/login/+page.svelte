<script>
    import TopBar from '../../components/TopBar.svelte';
    import {goto} from "$app/navigation";

    let email = "";
    let password = "";

    function login() {
        console.log("Login Successful!");
        localStorage.setItem('login', email);
        localStorage.setItem('password', password);
        goto('/');
    }
</script>
<TopBar/>

<main class="container-fluid d-flex align-items-center justify-content-center h-100">
    <div class="card p-4 shadow">
        <h1 class="mb-4">Login</h1>
        <form>
            <div class="mb-3">
                <label for="login-email" class="form-label">Email address</label>
                <input type="email" class="form-control" id="login-email" placeholder="Enter email" bind:value={email}>
            </div>
            <div class="mb-3">
                <label for="login-password" class="form-label">Password</label>
                <input type="password" class="form-control" id="login-password" placeholder="Enter password" bind:value={password}>
            </div>
            <div class="d-grid gap-2 col-6 mx-auto">
                <button type="button" class="btn btn-primary btn-lg" on:click={login}>Login</button>
            </div>
        </form>
    </div>
</main>

<style>
    @import 'bootstrap/dist/css/bootstrap.min.css';

    main {
        height: 100vh;
    }

    .card {
        max-width: 400px;
        border: 1px solid #ccc;
        border-radius: 8px;
    }
</style>
