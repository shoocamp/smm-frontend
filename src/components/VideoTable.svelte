<script>
    export let videos = [];

    function beautifyDateTime(dateTimeString) {
        const dateTime = new Date(dateTimeString);
        const options = {
            year: 'numeric',
            month: 'long',
            day: 'numeric',
            hour: 'numeric',
            minute: 'numeric',
            second: 'numeric'
        };
        const formattedDateTime = dateTime.toLocaleString(undefined, options);
        return formattedDateTime;
    }

</script>
<table class="table">
    <thead>
    <tr>
        <th>Title</th>
        <th>Description</th>
        <th>Platforms</th>
        <th>Time of Publish</th>
        <th>Status</th>
    </tr>
    </thead>
    <tbody>
    {#await videos}
        <p>Loading...</p>
    {:then videos}
        {#each videos as video}
            <tr>
                <td>{video.info.title}</td>
                <td>{video.info.description}</td>
                <td>
                    {#each video.target_platforms as platform}
                        {platform}
                    {/each}
                </td>
                <td>{beautifyDateTime(video.time_to_publish)}</td>
                <td>{video.status}</td>
            </tr>
        {/each}
    {/await}
    </tbody>
</table>
