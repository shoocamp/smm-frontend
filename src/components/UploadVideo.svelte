<script>
  let title = "";
  let description = "";
  let tags = [];
  let selectedPlatforms = [];

  let platforms = [
    { id: 1, name: "YouTube" },
    { id: 2, name: "Instagram" },
    { id: 3, name: "TikTok" },
    // Add more platforms as needed
  ];

  function handleTagsInput(event) {
    // Split tags input by comma and trim whitespace
    tags = event.target.value.split(",").map(tag => tag.trim());
  }

  function handlePlatformSelection(event) {
    selectedPlatforms = Array.from(event.target.selectedOptions, option => parseInt(option.value));
  }

  function handleFormSubmit(event) {
    event.preventDefault();

    // Perform form submission logic here
    const videoData = {
      title,
      description,
      tags,
      platforms: selectedPlatforms
    };

    console.log("Video Upload:", videoData);
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
    <div class="mb-3">
      <label for="platforms" class="form-label">Video Platforms</label>
      <select multiple class="form-select" id="platforms" on:change={handlePlatformSelection}>
        {#each platforms as platform}
          <option value={platform.id}>{platform.name}</option>
        {/each}
      </select>
    </div>
    <div class="d-grid gap-2 col-6 mx-auto">
      <button type="submit" class="btn btn-primary">Upload</button>
    </div>
  </form>
</main>

<style>
  @import 'bootstrap/dist/css/bootstrap.min.css';
</style>
