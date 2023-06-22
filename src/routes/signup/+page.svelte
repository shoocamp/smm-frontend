<script>
  import TopBar from '../../components/TopBar.svelte';

  let email = "";
  let password = "";
  let username = ""

  function register() {
    // Handle registration logic here
    console.log("Registration Successful!");
  }

</script>
<TopBar />

<main class="container mt-4">
  <form>
    <h2>Register</h2>
    <div class="mb-3">
      <label for="register-email" class="form-label">Username</label>
      <input type="email" class="form-control" id="register-username" bind:value={username} placeholder="Enter username">
    </div>
    <div class="mb-3">
      <label for="register-email" class="form-label">Email address</label>
      <input type="email" class="form-control" id="register-email" bind:value={email} placeholder="Enter email">
    </div>
    <div class="mb-3">
      <label for="register-password" class="form-label">Password</label>
      <input type="password" class="form-control" id="register-password" bind:value={password} placeholder="Enter password">
    </div>
    <button type="button" class="btn btn-primary" on:click={register}>Register</button>
  </form>

</main>

<style>
  @import 'bootstrap/dist/css/bootstrap.min.css';
</style>
