<script>
    import TopBar from '../../components/TopBar.svelte';
    import {goto} from "$app/navigation";

    let username = "";
    let password = "";

    function login() {
        event.preventDefault();

        const formData = new FormData();
        formData.append("username", username);
        formData.append("password", password);

        fetch('http://localhost:8000/api/v1/users/signin', {
            method: 'POST',
            body: formData
        })
            .then(response => {
                if (response.ok) {
                    response.json().then(
                        data => {
                            console.log(data);
                            localStorage.setItem('token', data['access_token']);
                            console.log('Sing-in successful');
                            goto('/');
                        }
                    )
                } else {
                    // Handle error cases
                    response.json().then(
                        data => {
                            console.error(`Sign-in failed: `, data);
                            alert(`Sign-in failed`)
                        }
                    )
                }
            })
            .catch(error => {
                console.error('An error occurred', error);
            });
    }

</script>
<TopBar/>

<main class="container-fluid d-flex align-items-center justify-content-center h-100">
    <div class="card p-4 shadow">
        <h1 class="mb-4">Login</h1>
        <form>
            <div class="mb-3">
                <label for="username" class="form-label">Email address</label>
                <input type="text" class="form-control" id="username" placeholder="Enter username" bind:value={username}>
            </div>
            <div class="mb-3">
                <label for="login-password" class="form-label">Password</label>
                <input type="password" class="form-control" id="login-password" placeholder="Enter password"
                       bind:value={password}>
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
