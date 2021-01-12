<script>
  import { onMount } from "svelte";
  import Soundboard from "./Soundboard.svelte";
  import SoundSearch from "./SoundSearch.svelte";
  export let name;

  let searchTerm = "";
  let sounds = [];
  let displayList = [];

  onMount(async () => {
    const res = await fetch(`soundboard.json`);
    sounds = await res.json();
    displayList = sounds.files;
  });

  function filterList(list, query) {
    displayList = sounds.files;
    return displayList.filter(item => {
      return (
        item.name.toLowerCase().match(query.toLowerCase()) ||
        item.artist.toLowerCase().match(query.toLowerCase())
      );
    });
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }
  h1 {
    color: rgb(1, 1, 59);
    font-size: 2em;
    font-weight: 100;
    margin: 0;
    text-align: center;
  }
  h2 {
    font-size: 1.3em;
    font-weight: 100;
    margin: 0;
    text-align: center;
  }
  div {
    margin: 0 auto;
  }
</style>

<svelte:head>
  <title>{name}</title>
  <meta name="description" content="">

  <!-- Facebook Meta Tags -->
  <meta property="og:url" content="https://botan.rocks/">
  <meta property="og:type" content="website">
  <meta property="og:title" content="botan.rocks - Your emergency Shishiro Botan noises button.">
  <meta property="og:description" content="">
  <meta property="og:image" content="https://botan.rocks/ogp-thumbnail.png">

  <!-- Twitter Meta Tags -->
  <meta name="twitter:card" content="summary_large_image">
  <meta property="twitter:domain" content="">
  <meta property="twitter:url" content="https://botan.rocks/">
  <meta name="twitter:title" content="botan.rocks - Your emergency Shishiro Botan noises button.">
  <meta name="twitter:description" content="">
  <meta name="twitter:image" content="https://botan.rocks/ogp-thumbnail.png">

  <!-- Meta Tags Generated via https://www.opengraph.xyz -->
</svelte:head>
<header>
  <h1>{name}</h1>
  <h2>made possible by the endless contributions of the <a target="_blank" href="https://discord.gg/ynSShd8">SSRB fan discord</a></h2>
</header>
<main>
  <section>
<!--     <SoundSearch
      bind:searchTerm
      on:updateSearch={() => {
        displayList = filterList(sounds, searchTerm);
      }} /> -->
    <Soundboard bind:sounds={displayList} />
  </section>
  <section>
    <p><a target="_blank" href="https://github.com/theabhishek2511/botan-rocks">view source on github</a> | powered by <a target="_blank" href="https://svelte.dev/">svelte</a>, <a target="_blank" href="https://www.netlify.com/">netlify</a> and <a target="_blank" href="https://www.cloudflare.com/">cloudflare</a> | <a target="_blank" href="https://twitter.com/omgitsnewton">site maintainer</a></p>
  </section>
</main>
