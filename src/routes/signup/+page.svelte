<script>
    import TopBar from '../../components/TopBar.svelte';
    import {goto} from "$app/navigation";

    let email = "";
    let password = "";
    let username = ""

    function register(event) {
        event.preventDefault();

        const formData = new FormData();
        formData.append("username", username);
        formData.append("password", password);
        formData.append("email", email);

        fetch('http://localhost:8000/api/v1/users/signup', {
            method: 'POST',
            body: formData
        })
            .then(response => {
                if (response.ok) {
                    response.json().then(
                        data => {
                            console.log(data);
                            localStorage.setItem('token', data['access_token']);
                            console.log('Sign-up successful');
                            goto('/');
                        }
                    )
                } else {
                    // Handle error cases
                    response.json().then(
                        data => {
                            console.error(`Sign-up failed: `, data);
                            alert(`Sign-up failed`)
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

<main class="container mt-4">
    <form on:submit={register}>
        <h2>Register</h2>
        <div class="mb-3">
            <label for="register-username" class="form-label">Username</label>
            <input type="text" class="form-control" id="register-username" bind:value={username}
                   placeholder="Enter username">
        </div>
        <div class="mb-3">
            <label for="register-email" class="form-label">Email address</label>
            <input type="email" class="form-control" id="register-email" bind:value={email} placeholder="Enter email">
        </div>
        <div class="mb-3">
            <label for="register-password" class="form-label">Password</label>
            <input type="password" class="form-control" id="register-password" bind:value={password}
                   placeholder="Enter password">
        </div>
        <button type="submit" class="btn btn-primary">Register</button>
    </form>

</main>

<style>
    @import 'bootstrap/dist/css/bootstrap.min.css';
</style>
