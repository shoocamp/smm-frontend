<script>
    import {goto} from "$app/navigation";

    let title = "";
    let description = "";
    let tags = [];
    let file = null;
    let vkCheckbox = false
    let youtubeCheckbox = false

    function handleFileChange(event) {
        file = event.target.files[0];
    }

    let platforms = [
        {id: 1, name: "YouTube"},
        {id: 2, name: "Instagram"},
        {id: 3, name: "TikTok"},
    ];

    function handleTagsInput(event) {
        // Split tags input by comma and trim whitespace
        tags = event.target.value.split(",").map(tag => tag.trim());
    }

    function handleFormSubmit(event) {
        event.preventDefault();

        // Perform form submission logic here

        const formData = new FormData();
        formData.append('file', file);
        formData.append('title', title);
        formData.append('description', description);
        formData.append('vk', vkCheckbox);
        formData.append('youtube', youtubeCheckbox);

        fetch('http://localhost:8000/api/v1/videos/', {
            method: 'POST',
            body: formData,
            headers: {
                "Authorization": `Bearer ${localStorage.getItem("token")}`
            }
        })
            .then(response => {
                if (response.ok) {
                    // Successful upload logic
                    console.log('File uploaded successfully');
                    goto('/videos');
                } else {
                    // Handle error cases
                    console.error('File upload failed');
                }
            })
            .catch(error => {
                console.error('An error occurred', error);
            });
    }
</script>

<main class="container-fluid">
    <h2>Upload Video</h2>

    <form on:submit={handleFormSubmit}>
        <div class="mb-3">
            <label for="title" class="form-label">Title</label>
            <input type="text" class="form-control" id="title" bind:value={title}>
        </div>
        <div class="mb-3">
            <label for="description" class="form-label">Description</label>
            <textarea class="form-control" id="description" rows="4" bind:value={description}></textarea>
        </div>
        <div class="mb-3">
            <label for="tags" class="form-label">Tags (comma-separated)</label>
            <input type="text" class="form-control" id="tags" on:input={handleTagsInput}>
        </div>
        <div class="form-check mb-3">
            <label class="form-check-label" for="vkCheck">VK</label>
            <input class="form-check-input" type="checkbox" id="vkCheck" bind:value={vkCheckbox}>
        </div>
        <div class="form-check mb-3">
            <label class="form-check-label" for="ytCheck">Youtube</label>
            <input class="form-check-input" type="checkbox" id="ytCheck" bind:value={youtubeCheckbox}>
        </div>
        <div class="mb-3">
            <label for="file" class="form-label">Select File</label>
            <input type="file" class="form-control" id="file" on:change={handleFileChange}/>
        </div>
        <div class="d-grid gap-2 col-6 mx-auto">
            <button type="submit" class="btn btn-primary">Upload</button>
        </div>
    </form>
</main>

<style>
    @import 'bootstrap/dist/css/bootstrap.min.css';
</style>
