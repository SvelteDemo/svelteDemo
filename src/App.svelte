<script>

  import KrisPage from './kris.svelte';
  import { Router, Route, Link } from "svelte-routing";
  import Three from './three.svelte';
  import Video from './video.svelte';
  export let url = ""

</script>
<Router url="{url}">
  <nav>
  <div>
    <Link to="/home">Home</Link>
  </div>
  <div>
   <Link to="kris">Pictures</Link>
  </div>
  <div>
   <Link to="three">Rick</Link>
  </div>
  <div>
   <Link to="video">Video/Audio</Link>
  </div>
  </nav>
  <div>
   <Route path="/home"></Route>
   <Route path="/kris" component="{KrisPage}" />
   <Route path="/three" component="{Three}" />
   <Route path="/video" component="{Video}" />
  </div>
</Router>

<main>

</main>

<style>

  nav{
    position: 'fixed';
    top: 0;

  }

</style>
