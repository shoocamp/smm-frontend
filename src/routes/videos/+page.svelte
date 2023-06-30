<script>
    import {onMount} from 'svelte';
    import TopBar from '../../components/TopBar.svelte';
    import VideoTable from '../../components/VideoTable.svelte';

    let videos = [];

    onMount(async () => {
        const response = await fetch('http://localhost:8000/api/v1/videos', {
            headers: {
                "Authorization": `Bearer ${localStorage.getItem("token")}`
            }
        });
        videos = await response.json();
        console.log(videos);
    });

</script>
<TopBar/>
<div class="container">
    <VideoTable {videos}/>
</div>
