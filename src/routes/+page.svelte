<script>
    import {writable} from "svelte/store"
    import {browser} from "$app/environment"
    import TopBar from '../components/TopBar.svelte';
    import UploadVideo from "../components/UploadVideo.svelte";

    let userIsLoggedIn = browser && localStorage.getItem("token");
</script>

<TopBar/>
<div class="container">
    {#if userIsLoggedIn}
        <UploadVideo/>
    {/if}
</div>
