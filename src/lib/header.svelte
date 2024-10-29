<script>
import {page} from '$app/stores'
import {meis} from '$lib'
import '$lib/app.css'
</script>
<header>
{#each meis as mei, i}
    <a href="/{mei === $page.params.mei ? `${mei}/1` : mei}" class="mei{mei}">
   <img src="/iiimages/{mei}-1.jpg" alt="wallpaper" />
   <!-- <img src="https://collections.newberry.org/IIIF3/Image/{mei}/full/50,200/0/default.jpg" alt="wallpaper" /> -->
    </a> 
{/each}
</header>

<style>
header {
  z-index: 90000;
  position: fixed;
  top: 3px;
  right: 3px;
  left: 3px;

  display: flex;
  gap: 3px;
  & * {
box-sizing: border-box;
  }

}
header a {
  overflow: hidden;

  height: 50px;
  width: 100%;
  border: 2px solid var(--background);
}
header img {
  height: 50px;
  width: 100%;
  object-fit: cover;
}
</style>
