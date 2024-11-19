<script>
  import App from '$lib/components/App.svelte'
</script>

<div id="kill-me">
  <App />
    <div id="kill-me-again">
      <h1>kill me</h1>
    </div>
</div>

<style>
  :global(body) {
    margin: 0;
  }

  #kill-me {
    position: relative;
    width: 100vw;
    height: 100vh;
    background: rgb(13, 19, 32);
    background: linear-gradient(180deg, rgba(13, 19, 32, 1) 0%, rgba(8, 12, 21, 1) 100%);
  }
</style>
