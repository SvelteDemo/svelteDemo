<script>
  import { crossfade, scale } from "svelte/transition";
  import App from "./App.svelte";
  import images from "./images.js";
  import handleShow from "./App.svelte";
  import { Router, Route, Link } from "svelte-routing";

  const [send, receive] = crossfade({
    duration: 200,
    fallback: scale,
  });

  let selected = null;
  let loading = null;
  let rickFact = [
    "Rick Astley’s 1987 song ‘Never Gonna Give You Up’, was released to critical acclaim. It reached No.1 in 25 countries",
    "Rick Astley started out as a choir boy at his local church.",
    "Rick Astley doesn't like to fly.",
    "His song 'Never Gonna Give You Up' reached 1 billion views in July 2021",
  ];
  let url="";
  //const ASSETS = `https://sveltejs.github.io/assets/crossfade`;

  const load = (image) => {
    const timeout = setTimeout(() => (loading = image), 100);
    const img = new Image();
    img.onload = () => {
      selected = image;
      clearTimeout(timeout);
      loading = null;
    };
    img.src = `/RAstley/${image.path}`;
  };
</script>

<div class="container">
  <div class="phone">
    <h1>' R _ _ K A s _ l _ y '</h1>

    <div class="grid">
      {#each images as image}
        <div class="square">
          {#if selected !== image}
            <button
              style="background-color: {image.color};"
              on:click={() => load(image)}
              in:receive={{ key: image.id }}
              out:send={{ key: image.id }}
              >{loading === image ? "..." : "Who Am I ?"}</button
            >
          {/if}
        </div>
      {/each}
      <div>
        <Router url="{url}">
          <nav>
            <button class="home_button">
              <Link to="/home" replace>Home</Link>
            </button>
          </nav>
        </Router>
      </div>
    </div>

    {#if selected}
      {#await selected then d}
        <div class="photo" in:receive={{ key: d.id }} out:send={{ key: d.id }}>
          <img
            alt={d.alt}
            src="/RAstley/{d.path}"
            on:click={() => (selected = null)}
            on:keydown={() => (selected = null)}
          />
          <p class="credit">
            {rickFact[d.id - 1]}
          </p>
        </div>
      {/await}
    {/if}
  </div>
</div>

<style>
  .container {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background-color: #242424;
  }

  .phone {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 52vmin;
    height: 76vmin;
    border: 2vmin solid #ccc;
    border-bottom-width: 10vmin;
    padding: 3vmin;
    border-radius: 2vmin;
  }

  h1 {
    font-weight: 300;
    text-transform: uppercase;
    font-size: 5vmin;
    margin: 0.2em 0 0.5em 0;
  }

  .grid {
    display: grid;
    flex: 1;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(2, 1fr);
    grid-gap: 2vmin;
  }

  button {
    width: 100%;
    height: 100%;
    color: white;
    font-size: 5vmin;
    border: none;
    margin: 0;
    will-change: transform;
  }

  .photo,
  img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .photo {
    display: flex;
    align-items: stretch;
    justify-content: flex-end;
    flex-direction: column;
    will-change: transform;
  }

  img {
    object-fit: cover;
    cursor: pointer;
  }

  .credit {
    text-align: left;
    font-size: 2vmin;
    padding: 1em;
    margin: 0;
    color: white;
    font-weight: bold;
    opacity: 0.6;
    background: rgba(0, 0, 0, 0.4);
  }
.home_button{
  border: solid 1px black;
  margin: 10px;
  padding: 5px;
  min-width: 200%;
}
  .credit a,
  .credit a:visited {
    color: white;
  }
</style>
