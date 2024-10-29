<script lang="ts">
import '$lib/app.css';
import {meis} from '$lib'
import textcontent from '$lib/textcontent.json'
import {page} from '$app/stores'
let ww = $state(1)
let wh = $state(1)
let pageParams = $page.params.mei.split('/')
let pathIndex  = $state( pageParams[1] || 0)
let mei = $state( pageParams[0] || meis[0])
let index = $state(meis.indexOf(mei))

let active = $state(0)
let content = $state(textcontent[index][pathIndex])
let gradient = ""

makeGradient(5, 1)
function makeGradient(n, offset) {
  let colors = Array.from({length: n}).map((_, i) => {
    let increment = 100 / n
    let start = Math.round( increment * i )
    let end =  Math.round( increment * (i + 1) )
    return ` rgb(var(--color${i + offset}), 0.5) ${start}% ${end}%`
  })
  gradient = `linear-gradient(${colors.join(",")});`
}

function getFontSize(a, ww, wh ){

  let r = ww / wh

  let h = Math.sqrt(a / r)
  let w = r * h

  let fw = ww / w;
  let fh = wh / h;
  let fontSize = (fh + fw) / 2 

  return Math.round( fontSize )
 
}
let fontSize = $derived(getFontSize(content.title.length, ww, wh))
$inspect("window width: " , ww)
$inspect("window height: " , wh)
$inspect("fontsize: " , fontSize)
</script>
<svelte:window bind:innerWidth={ww} bind:innerHeight={wh}/>
<main id="mei{mei}" on:click={() => active = (active + 1) % 3}>
  {#if pathIndex}
    <img src="/iiimages/{mei}-1.webp" alt="wallpaper" />
  {:else}
    <!-- <img src="https://collections.newberry.org/IIIF3/Image/{mei}/square/max/0/default.jpg" alt="wallpaper" /> -->
  {/if}
  <div class="quad {active > 0 ? 'active' : ''}" style="background-image: {gradient};">
    <h1 style="line-height: {fontSize * 0.8}px; font-size: {fontSize }px">{content.titleExt ? content.titleExt : ''}{content.title}</h1> 
      <div class="minimodal {active > 1 ? 'show' : ''}" >
      {#if content.text}
        <ol>
          {#each content.text as text}
            <li>{@html text}</li>
          {/each}
        </ol>
      {:else}
        <div class="image">
        {@html content.image}
        </div>
      {/if}
    </div>
  </div>
</main>

<style>
 :global(s) {
  color: color-mix(in oklab, var(--background), transparent);
}

h1 {
  margin: 1rem;
  font-size: max(9vh, 9vw);
  font-family: 'neon';
  word-break: break-all;
  text-align: justify;
  text-justify: distribute;
}

:global(body){
  background: #333;
  color: #ccc;
}

main {

  min-height: 101vh;
  background-image: var(--wallpaper);
  background-size: cover;
  background-position: center;
  background-attachment: fixed;

}
img {
  width: 100vw;
  height: 100vh;
  object-fit: cover;

}
.active {
  top: 0;
}
.quad:not( .active ) {
  top: 111vh;
}
.show {
  top: 0;
    bottom: 0;
}
.minimodal:not(.show){
  top: 111vh;
    bottom: -111vh;

}
.quad {
  opacity: 0.87;
   backdrop-filter: blur(10px); 
  position:absolute ;
  transition: top 500ms;
  overflow: hidden;
  box-shadow: 0 0 7px 7px color-mix(in oklab, var(--background), transparent);
  margin: 10vh 10vw;
  width: 80vw;
  height: 80vh;
  color: var(--background);
  /* background: rgb(var(--color2)); */
  border: 5px solid var(--foreground) ;
  border-radius: 5px;
    display: grid; 
    place-items: center;
  & h1 {
    margin: 0;
    padding: 0;
    font-size: 10vh;
  }
  & .minimodal {
    display: grid; 
    max-width: 66%;
    margin: auto;
    place-items: center;
    position: absolute;
    /* top: 0; */
    left: 0;
    right: 0;

   pointer-events: none;
  transition: top 500ms;
  }
  & ol {
     
    padding: 33px !important;
    /* margin: 30%; */
    /* height: 30%; */
    font-size: 33px;
     backdrop-filter: blur(10px);
    background: rgba(var(--color1), 0.87);
    border: 5px solid var(--background) ;
    border-radius: 5px 5px 0 0 ;
     /* margin: 0 0 -5px 0; */

    color: var(--background);
    & li {
     margin-inline: 33px;
    }
  }
  & .image {
     pointer-events: all;
    padding: 33px !important;
     backdrop-filter: blur(10px);
    background: rgba(var(--color1), 0.87);
    border: 5px solid var(--background) ;
    border-radius: 5px 5px 0 0 ;
   }

}
</style>
