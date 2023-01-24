<script>
  import Inputdata from './lib/Inputdata.svelte';
  import Header from './lib/Header.svelte';
</script>

<main>
  
  <div class="logo">
    <Header />
  </div>

  <div class="inputdata">
    <Inputdata />
  </div>

  <p class="read-the-docs">
    Click on the YT.AI logo to learn more
  </p>

  <div class="card">
    
  </div>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #9a7e7eaa);
  }
  .read-the-docs {
    color: #888;
  }
  .inputdata {
    padding: 8em;
  }
</style>
