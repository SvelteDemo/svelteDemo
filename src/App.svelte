<script>

  import KrisPage from './kris.svelte';
  import { Router, Route, Link } from "svelte-routing";
  import Three from './three.svelte';
  import Video from './video.svelte';
  export let url = ""

</script>
<Router url="{url}">
  <nav>
   <Link to="/">Home</Link>
   <Link to="kris">Pictures</Link>
   <Link to="three">Rick</Link>
   <Link to="video">Video/Audio</Link>
  </nav>
  <div>
   <Route path="/"></Route>
   <Route path="/kris" component="{KrisPage}" />
   <Route path="/three" component="{Three}" />
   <Route path="/video" component="{Video}" />
  </div>
</Router>

<main>
  <h1>Home Page</h1>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
