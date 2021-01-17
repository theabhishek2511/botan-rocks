<script>
  import { onMount } from "svelte";
  import Soundboard from "./Soundboard.svelte";
  import SoundSearch from "./SoundSearch.svelte";
  import Meta from "./Meta.svelte"
  export let name;

  let root = [];

  const metadata = {
    title: 'botan.rocks - Your emergency Shishiro Botan noises button.',
    description: '',
    image: 'https://botan.rocks/ogp-thumbnail.png',
    url:'https://botan.rocks/',
    type:'website'
  }

  onMount(async () => {
    const res = await fetch(`soundboard.json`);
    root = await res.json();
  });

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
  section {
    margin-bottom: 2em
  }
</style>

<Meta {metadata}/>

<header>
  <h1>{name}</h1>
  <h2>made possible by the endless contributions of the <a target="_blank" href="https://discord.gg/ynSShd8">SSRB fan discord</a></h2>
</header>
<main>
  {#each root as { name, files }}
  <section>
    <h2>{name}</h2>
    <Soundboard bind:sounds={files} />
  </section>
  {/each}
<!--   <section>
    <Soundboard bind:sounds={displayList2} />
  </section>
  <section>
    <Soundboard bind:sounds={displayList1} />
  </section> -->
  
  <p><a target="_blank" href="https://github.com/theabhishek2511/botan-rocks">view source on github</a> | powered by <a target="_blank" href="https://svelte.dev/">svelte</a>, <a target="_blank" href="https://www.netlify.com/">netlify</a> and <a target="_blank" href="https://www.cloudflare.com/">cloudflare</a> | <a target="_blank" href="https://twitter.com/omgitsnewton">site maintainer</a></p>
</main>
