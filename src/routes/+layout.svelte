<script>
  import { fade, fly } from 'svelte/transition'
import Header from '$lib/header.svelte'
  export let data

    // in:fade={{ duration: 500 }} out:fade={{duration: 500}}
</script>
<Header />

{#key data.url}
  <div
in:fade={{ duration: 300 }}
    out:fly={{ duration: 300 }}
  >
    <slot />
  </div>
{/key}
