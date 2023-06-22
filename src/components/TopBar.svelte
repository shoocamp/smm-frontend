<script>
    import {browser} from "$app/environment";
    import {goto} from "$app/navigation";

    let userIsLoggedIn = browser && localStorage.getItem("login") && localStorage.getItem("password");

    function logOut() {
        localStorage.removeItem('login');
        localStorage.removeItem('password');
        userIsLoggedIn = null
        goto('/');
    }

    let showDropdown = false;

    function toggleDropdown() {
        showDropdown = !showDropdown;
    }

</script>

<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
        <a class="navbar-brand" href="/">SMM Successor</a>
        <div class="collapse navbar-collapse">
            <ul class="navbar-nav ms-auto">
                {#if userIsLoggedIn}
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" role="button" on:click={toggleDropdown}>
                            {browser && localStorage.getItem("login")}
                        </a>
                        {#if showDropdown}
                            <div class="dropdown-menu dropdown-menu-end show">
                                <a class="dropdown-item" href="/preference">Profile</a>
                                <div class="dropdown-divider"></div>
                                <button class="dropdown-item" on:click={logOut}>Logout</button>
                            </div>
                        {/if}
                    </li>
                {/if}
                {#if !userIsLoggedIn}
                    <li class="nav-item">
                        <a class="nav-link" href='/login'>Login</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href='/signup'>Sign Up</a>
                    </li>
                {/if}
            </ul>
        </div>
    </div>
</nav>

<style>
    @import 'bootstrap/dist/css/bootstrap.min.css';
</style>
