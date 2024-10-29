<script>
import Arrow from './arrow.svelte'

let { content, active } = $props()
$inspect(content.text)

let show = $state(-1)

</script>
<style>
</style>
