<script>
    import {browser} from "$app/environment";
    import {goto} from "$app/navigation";
    import {onMount} from 'svelte';

    let userIsLoggedIn = browser && localStorage.getItem("token");

    function logOut() {
        localStorage.removeItem('token');
        userIsLoggedIn = null
        goto('/');
    }

    onMount(async () => {
        if (browser && localStorage.getItem("token")) {
            fetch('http://localhost:8000/api/v1/users/info', {
                method: 'GET',
                headers: {
                    "Authorization": `Bearer ${localStorage.getItem("token")}`
                }
            })
                .then(response => {
                    if (response.ok) {
                        response.json().then(
                            data => {
                                console.log(data);
                                localStorage.setItem('username', data['username']);
                            }
                        )
                    } else {
                        // Handle error cases
                        response.json().then(
                            data => {
                                console.error(`Get info failed: `, data);
                                // alert(`Get info failed`)
                            }
                        )
                    }
                })
                .catch(error => {
                    console.error('An error occurred', error);
                });
        }
    })


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
                    <li class="nav-item">
                        <a class="nav-link" href='/videos'>my videos</a>
                    </li>
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" role="button" on:click={toggleDropdown}>
                            {browser && localStorage.getItem("username")}
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
