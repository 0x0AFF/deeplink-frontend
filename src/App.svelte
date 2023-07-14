<script>
  import "carbon-components-svelte/css/g80.css";
  import { Button, TextInput, Tile } from "carbon-components-svelte";
  import CloseFilled from "carbon-icons-svelte/lib/CloseFilled.svelte";
  import { onMount } from "svelte";

  let deeplink = "";

  const handleClick = () => {
    localStorage.setItem("deeplink", deeplink);
    window.location.assign(deeplink);
  };

  const handleDeleteClick = () => {
    deeplink = "";
    localStorage.setItem("deeplink", deeplink);
  };

  onMount(() => {
    const link = localStorage.getItem("deeplink");
    if (link) {
      deeplink = link;
    }
  });
</script>

<main>
  <Tile>
    <div class="container">
      <TextInput
        labelText="Deeplink"
        placeholder="Enter deeplink..."
        bind:value={deeplink}
      /><Button
        on:click={handleDeleteClick}
        kind="danger-tertiary"
        iconDescription="Delete"
        icon={CloseFilled}
      />
    </div>
    <br />
    <Button on:click={handleClick} kind="secondary">Open deeplink</Button>
  </Tile>
</main>

<style>
  :global(.bx--tile) {
    width: 100%;
    max-width: 400px;
  }

  :global(.bx--form-item) {
    padding-right: 15px;
  }

  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
</style>
